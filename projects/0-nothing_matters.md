---
layout: page
title: nothing_matters
description: video game
image: assets/images/nothing_matters.png
nav-menu: true
---
<div id="main" class="alt">
<div class="inner">

{% highlight hlsl %}
struct appdata {
    float4 vertex : POSITION;
    float2 uv : TEXCOORD0;
};

struct v2f {
    float2 uv : TEXCOORD0;
    float2 wPos : TEXCOORD1;
    float4 vertex : SV_POSITION;
};

sampler2D _MainTex;
float4 _MainTex_ST;
fixed4 _ScanLineTint;
float _ScanlineCount;
float _ScanlineCount2;
float _ScanlineSpeed;
float _ScanlinePerterbationSpeed;
float _ScanLineVisibility;
float _ScanLineUVStrength;

float _ChromaticAberrationAmount;

float _UV_Y_Offset;

v2f vert (appdata v) {
    v2f o;
    o.vertex = UnityObjectToClipPos(v.vertex);
    o.uv = TRANSFORM_TEX(v.uv, _MainTex);
    o.wPos = TransformObjectToWorld(v.vertex);

    return o;
}

fixed4 frag (v2f i) : SV_Target {
    // for scroll screen as another "glitched" effect
    i.uv.y += _UV_Y_Offset;

    // Scanlines
    fixed4 scanLine1 = frac((i.uv.y + _Time.x * _ScanlineSpeed) * _ScanlineCount);
    fixed4 scanLine2 = frac((i.wPos.y + _Time.x * 0.5 * _ScanlineSpeed) * _ScanlineCount2);
    // Generate third oscillating scan line to purterbate other two scanlines
    //fixed4 scanLine3 = frac((i.wPos.y + _Time.x) * (sin(_Time.x * _ScanlinePerterbationSpeed) * 10 + 10));

    fixed4 scanLines = scanLine1 * scanLine2 * _ScanLineTint;

    // uv distortion by scanlines
    i.uv += 0.01 * scanLines * _ScanLineUVStrength; 

    // Chromatic Aberration
    fixed s = 0.001 * (_ChromaticAberrationAmount + scanLines * 2);
    fixed r = tex2D(_MainTex, i.uv + fixed2(+s, +s)).r;
    fixed g = tex2D(_MainTex, i.uv + fixed2(+s, -s)).g;
    fixed b = tex2D(_MainTex, i.uv + fixed2(-s, -s)).b;
    fixed4 col = tex2D(_MainTex, i.uv);
    fixed4 aberratedColor = fixed4(r, g, b, col.a);

    // Luminance threshold for scanline visibility
    fixed4 originalColor = tex2D(_MainTex, i.uv);
    float luminance = (0.2126f * originalColor.r + 0.7152f * originalColor.g + 0.0722f * originalColor.b);

    fixed4 finalColor = aberratedColor + (scanLines * luminance * _ScanLineVisibility * (1 - aberratedColor.a));
    return finalColor;
}
{% endhighlight %}

</div>
</div>