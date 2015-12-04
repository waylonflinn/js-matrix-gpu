1. can we do bigger than 2048?

2. can we do without the canvas element?

3. can we do float64?

4. how do we test against asm.js performance?

## GEMM
[Why GEMM is at the heart of deep learning](http://petewarden.com/2015/04/20/why-gemm-is-at-the-heart-of-deep-learning/)

## ASM.js
[Examples](http://www.2ality.com/2013/02/asm-js.html)
[Spec](http://asmjs.org/spec/latest/)

### Math.fround
[Introduction](https://hacks.mozilla.org/2013/12/gap-between-asm-js-and-native-performance-gets-even-narrower-with-float32-optimizations/)
[Examples](https://blog.mozilla.org/javascript/2013/11/07/efficient-float32-arithmetic-in-javascript/)

## Ostrich
[Ostrich Github](https://github.com/Sable/Ostrich)
[Using JavaScript and WebCL for Numerical Computations: A Comparative Study of Native and Web Technologies](https://ericklavoie.com/pubs/dls2014.pdf)

# new benchmark targets

## blis
https://github.com/flame/blis/tree/master/config/emscripten


# other related libraries

## furious
https://github.com/amd/furious.js/tree/master

## Yangqing Jia PhD Thesis
http://www.eecs.berkeley.edu/Pubs/TechRpts/2014/EECS-2014-93.pdf

# Answers

## QUESTION 1.
Chrome used to has a limit on canvas WebGL backbuffers?
tried to remove in April
[Removed arbitrary 4096 size limit on WebGL canvas backbuffers](https://groups.google.com/a/chromium.org/forum/#!topic/blink-reviews/BAh9eVgSwDI)

[Maximum size of a <canvas> element](http://stackoverflow.com/questions/6081483/maximum-size-of-a-canvas-element) (stackoverflow)

## QUESTION 3.

### float32 is probably enough
http://petewarden.com/2015/05/23/why-are-eight-bits-enough-for-deep-neural-networks/

### more investigation

var gl = g_m.__gpumatrix__;

gl.getShaderPrecisionFormat(this.gl.FRAGMENT_SHADER, this.gl.HIGH_FLOAT);

matches

High: precision = 23, range = 127 to 127 (exceeds spec)

from

http://stackoverflow.com/questions/4414041/what-is-the-precision-of-highp-floats-in-glsl-es-2-0-for-iphone-ipod-touch-ipad

Fused Multiply-Add could be used to increase precision in calculation, but doesn't seem to be part of WebGL yet
https://www.khronos.org/opengles/sdk/docs/man32/html/fma.xhtml
(WebGL uses opengl es shader language 1.0, https://www.khronos.org/registry/webgl/specs/1.0/#4.3)

Possible double precision gotcha
https://www.opengl.org/discussion_boards/showthread.php/183810-GLSL-double-precision-range?s=ab62584db8bb6499cd2a6ea9d866fa8d&p=1258355&viewfull=1#post1258355
