# softRenderer

I implement a CPU-based software rendering pipeline system from scratch using modern computer graphics theory. The system provides interfaces for image input and output, and is platform-independent. It includes a mathematical template library with various mathematical operations for vectors and matrices, as well as a complete rendering pipeline. During the design process, I implemented a shader interface to facilitate the implementation of additional effects, while ensuring that the code structure is clear and the modules are well-divided, making the system easy to maintain and modify.

![renderer](http://jinjinhe2001.github.io/images/renderer.png)
## Example shader code for Blinn-Phong in our system.  
```
Color Shader::FragmentShader()
{
        Vector3f l = vector_normalize(light.GetLightV(viewPos));
        Vector3f lightIntensity = light.GetIntensity();
        Vector3f eyePos = { 10, 0, 0 };
        Vector3f h = (l + eyePos) / vector_length_square(l + eyePos);
        float ka = 1.f, kd = 1.f, ks = 1.f;
        float r = vector_length_square(l);
        int p = 1;
        Vector3f la = ka * lightIntensity;
        Vector3f ld = kd * (lightIntensity / (r * r)) * std::max(0.f, vector_dot(normal, l));
        Vector3f ls = ks * (lightIntensity / (r * r)) * (float)std::pow(std::max(0.f, vector_dot(normal, h)),p);
        Vector3f L = la + ld + ls;

        Color textureColor = texture->GetColor(uvCoord.u, uvCoord.v);
        return Color(color.r * L[0] * textureColor.r, color.g * L[1] * textureColor.g, color.b * L[2] * textureColor.b);
}
```
