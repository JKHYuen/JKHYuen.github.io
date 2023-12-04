---
layout: page
permalink: /bloom-attenuation
title: Bloom Attenuation
description: My solution to common issues with the bloom post processing effect
image: assets/images/bloomAttenuation.png
page-banner: assets/images/bloom-page-banner.jpg
nav-menu: true

button-url: https://github.com/JKHYuen/BloomAttenuationBuild
button-text: Download Tech Demo

date-text: November 2021 — December 2021
---

<div class=nav>
<h4>Contents</h4>
<ul>
    <li><a href="#overview" class="button small scrolly"><span class="number">1.</span> Overview</a></li>
    <li><a href="#highlights" class="button small scrolly"><span class="number">2.</span> Highlights</a></li>
    <li><a href="#shader" class="button small scrolly"><span class="number">3.</span> Implementation</a></li>
    	<li><a href="#other-shaders" class="button small scrolly sub-section"><span class="number">3.1</span> Other Shaders</a></li>
</ul>
</div>

<header id="overview" class="major page-header"><h1><span class="number">1.</span> Overview</h1></header>

<video class="embedded-video" muted controls playsinline loop poster="{{ site.baseurl }}/assets/images/bloomAttenuation.png">
  <source src="{{ site.baseurl }}/assets/videos/bloom-preview.mp4" type="video/mp4">
  bloom preview video
</video>

This is my custom shader implementation of bloom to make the popular post processing effect more appealing. The shader simulates light fall off in the post processing step by using the camera depth texture as a bloom intensity multiplier, I call this solution "bloom attenuation". This effectively prevents bloom from oversaturating the screen and better differentiates bright objects with different distances from the player camera. Try the <a href="https://github.com/JKHYuen/BloomAttenuationBuild" target="_blank" rel="noopener noreferrer">playable tech demo</a> to change the bloom shader parameters and see the individual bloom rendering steps in real time!

See video below for a full project explanation.
<div id="video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/u5lX2zunj7g" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>

<header id="highlights" class="major page-header"><h1><span class="number">2.</span> Highlights</h1></header>
<ul class="highlights-list">
    <li>Novel bloom solution, implemented from scratch</li>
    <li>Extensive Cg/HLSL shader and graphics rendering work, with C# programming for demo game logic</li>
    <li>Playable <a href="https://github.com/JKHYuen/BloomAttenuationBuild" target="_blank" rel="noopener noreferrer">Unity tech demo</a>
		<ul class="highlights-list sub">
			<li>Adjust all bloom shader parameters and see individual rendering steps with a custom UI in real time</li>
			<li>Experience the effect with a custom first person controller</li>
			<li>On rails demo camera (as shown in video) to adjust parameters on the move</li>
		</ul>
	</li>
    <li>Project overview <a href="#video" class="scrolly">video</a>
		<ul class="highlights-list sub">
			<li>Scripting, video editing, and narration</li>
			<li>Full explanation of how post processing bloom works, with animated diagrams</li>
			<li>Tech and game design analysis of bloom use in other games</li>
		</ul>
	</li>
</ul>

<header id="shader" class="major page-header"><h1><span class="number">3.</span> Implementation</h1></header>
This project was done in Unity 2019, using the built-in render pipeline. To apply the depth bloom intensity multiplier, post processing bloom had to be implemented from scratch. This is done with a Cg/HLSL multi-pass bloom shader applied to the main camera's final image using Unity's ```OnRenderImage()``` function in C#.

<h4>Snippet of Custom Bloom Shader</h4>
{% highlight hlsl linenos %}
half3 Sample(float2 uv) {
	return tex2D(_MainTex, uv).rgb;
}

half3 SampleBox(float2 uv, float delta) {
	float4 o = _MainTex_TexelSize.xyxy * float2(-delta, delta).xxyy;
	half3 s =
		Sample(uv + o.xy) + Sample(uv + o.zy) +
		Sample(uv + o.xw) + Sample(uv + o.zw);
	return s * 0.25f;
}

half3 Prefilter(half3 c) {
	half brightness = max(c.r, max(c.g, c.b)); // brightness is max of color channels
	half soft = brightness - _Filter.y;
	soft = clamp(soft, 0, _Filter.z);
	soft = soft * soft * _Filter.w;
	half contribution = max(soft, brightness - _Filter.x);
	contribution /= max(brightness, 0.00001);
	return c * contribution;
}

float GetDistanceFromCamera(float2 uv) {
	return tex2D(_DepthTexture, uv);
}

SubShader{
	Cull Off
	ZTest Always
	ZWrite On

	Pass { // 0 - Prefilter + first downsample
		CGPROGRAM
			#pragma vertex VertexProgram
			#pragma fragment FragmentProgram

			half4 FragmentProgram(Interpolators i) : SV_Target{
				return max(lerp(1, GetDistanceFromCamera(i.sPos), _Attenuation), _MaxBloomReduction) * half4(Prefilter(SampleBox(i.uv, 1)), 1);
			}
		ENDCG
	}

	Pass { // 1 - downsample
		CGPROGRAM
			#pragma vertex VertexProgram
			#pragma fragment FragmentProgram

			half4 FragmentProgram(Interpolators i) : SV_Target{
				return half4(SampleBox(i.uv, 1), 1);
			}
		ENDCG
	}

	Pass { // 2 - upsample
		Blend One One // additive blend
		CGPROGRAM
			#pragma vertex VertexProgram
			#pragma fragment FragmentProgram

			half4 FragmentProgram(Interpolators i) : SV_Target {
				return half4(SampleBox(i.uv, 0.5), 1);
			}
		ENDCG
	}

	Pass { // 3 - final upsample + bloom addition
		CGPROGRAM
			#pragma vertex VertexProgram
			#pragma fragment FragmentProgram

			half4 FragmentProgram(Interpolators i) : SV_Target {
				half4 c = tex2D(_SourceTex, i.uv);
				c.rgb += _Intensity * SampleBox(i.uv, 0.5);
				return c;
			}
		ENDCG
	}

	Pass { // 4 - Bloom Debug
		CGPROGRAM
			#pragma vertex VertexProgram
			#pragma fragment FragmentProgram

			half4 FragmentProgram(Interpolators i) : SV_Target {
				return _Intensity * half4(SampleBox(i.uv, 0.5), 1);
			}
		ENDCG
	}

	Pass { // 5 - Depth Debug
		Tags { "RenderType" = "Opaque" }

		CGPROGRAM
			#pragma vertex VertexProgram
			#pragma fragment FragmentProgram

			half4 FragmentProgram(Interpolators i) : SV_Target {
				return GetDistanceFromCamera(i.sPos);
			}
		ENDCG
	}
}
{% endhighlight %}
*Note: Bloom attenuation is applied in line 38, a ```max(...)``` function with a tweakable ```_MaxBloomReduction``` variable is added so very far objects can still have bloom if desired (e.g. the moon). See <a href="#video" class="scrolly">video</a> for full details.*

<h4>Applying the Screen Shader in C#</h4>
{% highlight csharp linenos %}
private void OnRenderImage(RenderTexture source, RenderTexture destination) {
	if(bloom == null) {
		bloom = new Material(bloomShader);
		bloom.hideFlags = HideFlags.HideAndDontSave;
	}

	bloom.SetFloat("_Attenuation", attenuation);
	bloom.SetFloat("_MaxBloomReduction", maxBloomReduction);
	depthTextureRender.UpdateDepthCamFarPlaneScale(attenuationDistanceScale);

	if(isDebug_showDepthOnly) {
		Graphics.Blit(source, destination, bloom, DebugDepthPass);
		return;
	}

	float knee = threshold * softThreshold;
	Vector4 filter;
	filter.x = threshold;
	filter.y = filter.x - knee;
	filter.z = 2f * knee;
	filter.w = 0.25f / (knee + 0.00001f);
	bloom.SetVector("_Filter", filter);
	bloom.SetFloat("_Intensity", intensity);

	bloom.SetTexture("_DepthTexture", depthTexture);

	int width = source.width / 2;
	int height = source.height / 2;
	RenderTextureFormat format = source.format;

	// First downsampling iteration
	RenderTexture currentDestination = RenderTexture.GetTemporary(width, height, 0, format);
	textures[0] = currentDestination;

	Graphics.Blit(source, currentDestination, bloom, BoxDownPrefilterPass);
	RenderTexture currentSource = currentDestination;

	// Progressive Downsampling
	int i = 1;
	for(; i < iterations; i++) {
		width /= 2;
		height /= 2;

		if(height < 2) {
			break;
		}

		currentDestination = RenderTexture.GetTemporary(width, height, 0, format);
		textures[i] = currentDestination;

		Graphics.Blit(currentSource, currentDestination, bloom, BoxDownPass);
		currentSource = currentDestination;
	}

	// Progressive Upsampling
	for(i -= 2; i >= 0; i--) {
		currentDestination = textures[i];
		textures[i] = null;
		Graphics.Blit(currentSource, currentDestination, bloom, BoxUpPass);
		RenderTexture.ReleaseTemporary(currentSource);
		currentSource = currentDestination;
	}

	if(isDebug_showBloomContributionOnly) {
		Graphics.Blit(currentSource, destination, bloom, DebugBloomPass);
	}
	else {
		bloom.SetTexture("_SourceTex", source);
		Graphics.Blit(currentSource, destination, bloom, FinalBloomUpPass);
	}

	RenderTexture.ReleaseTemporary(currentSource);
}
{% endhighlight %}

<header id="other-shaders" class="page-header"><h2><span class="number">3.1</span> Other Shaders</h2></header>
<h4>Depth Camera Shader</h4>
Since we are using the default forward renderer, a second camera is needed to render depth into a render texture. This texture is sampled in the bloom shader as the attenuation multiplier. Having a second camera also allows us to fine tune the attenuation distance scale (i.e. set the distance where attenuation is max, with zero bloom) by setting the far plane distance of the depth camera independently from the main camera. This can be adjusted in real time with the "Distance Scale" parameter in the tech demo. 
{% highlight hlsl linenos %}
half4 frag(v2f i) : SV_Target {
	return 1 - Linear01Depth(tex2Dproj(_CameraDepthTexture, UNITY_PROJ_COORD(i.scrPos)));
}
{% endhighlight %}
Linear depth was used for this tech demo for simplicity, but the default non-linear depth would perhaps provide a more realistic inverse square law approximation for light attenuation. The depth value is also inversed since the Unity render engine uses reversed z values.

<h4>Moon Billboard</h4>
The moon in the tech demo is rendered as a relatively far away billboard sprite. This is done as opposed to using a skybox texture so we can better fine tune bloom intensity and make it look like a far away object at the same time.
{% highlight hlsl linenos %}
v2f vert(appdata v) {
	v2f o;
	o.pos = UnityObjectToClipPos(v.vertex);
	o.uv = v.uv.xy;

	// billboard mesh towards camera
	float3 vpos = mul((float3x3)unity_ObjectToWorld, v.vertex.xyz);
	float4 worldCoord = float4(unity_ObjectToWorld._m03, unity_ObjectToWorld._m13, unity_ObjectToWorld._m23, 1);
	float4 viewPos = mul(UNITY_MATRIX_V, worldCoord) + float4(vpos, 0);
	float4 outPos = mul(UNITY_MATRIX_P, viewPos);

	o.pos = outPos;

	o.vertColor = v.vertColor;

	return o;
}
{% endhighlight %}



