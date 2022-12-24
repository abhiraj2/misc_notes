## Raytracer
<hr>
#### PPM
<hr>

```
P3
3 2
255
255	0	0
0	255	0
0	0	255

255	255	0
255	0	255
0	255	255
```

First line tells that each pixel is 3 units long
Second line informs about the number of columns and rows
Third line tells the max value each param can take
Rest are pixel info

<hr>
#### Vec3 Class
<hr>
Contains three variables x,y,z

```
#include<iostream>

#include<cmath>

#define _VEC3 VEC3

class VEC3{

    public:

        VEC3(){}

        VEC3(float x1, float y1, float z1){x = x1; y=y1; z=z1;}

        float x,y,z;

        VEC3 operator-(){return VEC3(-x, -y, -z);}

        VEC3 operator+(){return *this;}

        VEC3& operator+=(VEC3& v2);

        VEC3& operator-=(VEC3& v2);

        VEC3& operator*=(VEC3& v2);

        VEC3& operator/=(VEC3& v2);

        VEC3& operator+=(const float f2);

        VEC3& operator-=(const float f2);

        VEC3& operator*=(const float f2);

        VEC3& operator/=(const float f2);

  

        float operator[](int i){

            if(i==0) return x;

            if(i==1) return y;

            if(i==2) return z;

        }

  

        void normalize();

        float magnitude();

};

  
  

float dot(VEC3& v1, VEC3& v2);

VEC3 cross(VEC3& v1, VEC3& v2);

  

std::ostream& operator<<(std::ostream& ost, VEC3 v);

  

std::istream& operator>>(std::istream& ist, VEC3 v);

  

VEC3 operator+(VEC3& v1, VEC3& v2);

VEC3 operator-(VEC3& v1, VEC3& v2);

VEC3 operator*(VEC3& v1, VEC3& v2);

VEC3 operator/(VEC3& v1, VEC3& v2);

VEC3 operator+(VEC3& v1, float& f2);

VEC3 operator-(VEC3& v1, float& f2);

VEC3 operator*(VEC3& v1, float& f2);

VEC3 operator/(VEC3& v1, float& f2);
```

**After we define vector class, we can utilize it in making ppm files
```
#ifndef _VEC3

    #include "vec3.h"

#endif

  

#include<fstream>

using namespace std;

int main(){

  

    fstream ppm;

    ppm.open("img.ppm", ios::out);

  

    ppm << "P3\n200 200\n 255\n";

    int row  = 200;

    int col = 200;

    float max = 255.0f;

    VEC3 color;

  

    for(int i=row-1; i>=0; i--){

        for(int j=0; j<col; j++){

            color = VEC3(float(j)/col, float(i)/row, 0.2f);

            color*=255.99f;

            ppm << color << "\n";

        }

    }

   return 0;  

}
```

<hr>
### Rays, a simple camera, and background
<hr>
Computation of colors in a raytracer happens along the direction of a ray.
Function of the ray, let `p(t) = A + t*B`, p is any 3D position along the ray. A is the starting point of the ray and B is the direction of the ray.

Every raytracer has a `color(ray)` function that interpolates the colors across the screen.

<hr>
### Adding DEM Spheres
<hr>
Equation of a spehere centered at origin with radius R, is
`x*x + y*y + z*z = R*r`
Same sphere, if located at center `(cx, cy, cz)`
`(x-cx)(x-cx) + (y-cy)(y-cy)+ (z-cz)(z-cz)`

The same thing in vector form becomes,
Taking `P = (x,y,z)`
`C = (cx, cy, cz)`
and `dot(P-C, P-C)` has the value `(x-cx)(x-cx) + (y-cy)(y-cy)+ (z-cz)(z-cz)` which is equal to `R*R`

Therefore the equation of a sphere in Vector form is `dot(P-C,P-C) = R*R`

Instead of P, we use our ray as `P(t)` and check where and all the above equation becomes true

Expanding the above formula with `P(t) = A + B*t`

we get `(A+B*t-C)(A+B*t-C) = (A-C)(A-C) + 2*(A-C)*B*t + (B*B)t*t - R*R = 0`
which is a quadratic in t, therefore easily solvable

### But you ask, what about DEM NORMALS??
Normal is a vector that is perpendicular to the surface and by convention points out.
For spheres specifically normals point outwards from hitpoint, in the direction of center, so if `P` is point and `C` is the center then, `P-C` is the normal 
```
rec.N = rec.P - this->center;
rec.N.normalize();
```

<hr>
### Anti Aliasing
<hr>
It is the process of reducing the jaggedness around the edges of a color change, mostly done by averaging a bunch of samples inside a pixel and by putting the color of pixel equal to the average.
For our general purpose raytracers stratification is not critical. We make use of a random number generator to average out the samples, with the number of samples per pixel as 100(say).

*Insert Images here of before and after AA*

<hr>
### Diffuse Materials
<hr>
Our implementation will have shapes and materials as separate, so that we can form combinatorics.

Light rays that are incident on Diffuse Materials, the rays get reflected in different directions. Algorithm for computing color for this is as follows

Pick a point S on the unit sphere, which is tangent on the hitpoint P (the sphere is tangent).
Get another random point R inside a unit sphere at the origin, then `P+N+R` will give the point S as P+N is the center and R is the point on the sphere with P as tangent due to parallelogram law, and on each hit the material will absorb 50% of the light incident.

```
VEC3 random_point_sphere(){

    VEC3 p;

    do{

        p = 2*VEC3(random_float(), random_float(), random_float()) - VEC3(1,1,1);

    }while(p.magnitude()*p.magnitude() >=1.0);

    return p;

}

  

VEC3 color(const RAY& r, hitable* world){

    hitpoint rec;

  

    if(world->hit_check(r, 0.0f, 9999999.0f, rec)){

        VEC3 target = rec.P + rec.N + random_point_sphere();

        //cout << target << endl;

        return 0.5*color(RAY(rec.P, (target - rec.P)), world);

    }

    else{

        VEC3 dir = r.direction();

        dir.normalize();

        float t = 0.5*(dir.y + 1);

        return VEC3(0.5f, 0.7f, 1.0f)*t + VEC3(1.0f, 1.0f, 1.0f)*(1.0f-t);

    }

  

}
```

In reality this sphere should be light grey. The dark in the color is due to the gamma correction being assumed by most image viewers. Just for approximation, we apply a gamma of 2, meaning raising colors to the power of 1/2.

