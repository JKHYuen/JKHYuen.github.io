---
layout: page
title: Bloom Attenuation
description: A solution to common issues with the bloom post processing effect.
image: assets/images/bloomAttenuation.png
nav-menu: true

button-url: https://github.com/JKHYuen/BloomAttenuationBuild
button-text: Download Tech Demo
---

<div class=nav>
<h4>Contents</h4>
<ul>
    <li><a href="#overview" class="button small scrolly">Overview</a></li>
    <li><a href="#shader" class="button small scrolly">Implementation</a></li>
</ul>
</div>

<header id="overview" class="major"><h3>Project Overview</h3></header>
<section id="video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/u5lX2zunj7g" title="YouTube video player" allowfullscreen></iframe>
</div>
</section>

My custom shader implementation of bloom to make the popular post processing effect more appealing. I call this solution "bloom attenuation", the shader simulates light fall off in the post processing step by using the camera depth texture as a bloom intensity multiplier. This effectively prevents bloom from oversaturating the screen and better differentiates bright objects with different distances from the player camera. See video above for a full project and implementation overview.

Try the <a href="https://github.com/JKHYuen/BloomAttenuationBuild" target="_blank" rel="noopener noreferrer">playable tech demo</a> to change the bloom shader parameters and see the individual bloom rendering steps in real time!

<header id="shader" class="major"><h3>Implementation</h3></header>
{% highlight hlsl linenos %}
Shader "Custom/Bloom" {
	Properties{
		_MainTex("Texture", 2D) = "white" {}
	}

	CGINCLUDE
		#include "UnityCG.cginc"

		sampler2D _MainTex, _SourceTex;
		sampler2D _DepthTexture;

		float4 _MainTex_TexelSize;
		half4 _Filter;
		half _Intensity;

		half _Attenuation;
		half _AttenuationStrength;
		half _MaxBloomReduction;

		struct VertexData {
			float4 vertex : POSITION;
			float2 uv : TEXCOORD0;
			float4 sPos : TEXCOORD1;
		};

		struct Interpolators {
			float4 pos : SV_POSITION;
			float2 uv : TEXCOORD0;
			float4 sPos : TEXCOORD1;
		};

		Interpolators VertexProgram(VertexData v) {
			Interpolators i;
			i.pos = UnityObjectToClipPos(v.vertex);
			i.sPos = ComputeScreenPos(i.pos);
			i.uv = v.uv;
			return i;
		}

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

	ENDCG

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
}
{% endhighlight %}








