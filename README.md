#include "colors.inc"
#include "golds.inc"

camera {
 location <1, 10, -35>
   look_at <8, 6.5, 0>
  angle 45
}

background { color rgb<0.2, 0.4, 0.8> }
light_source { <100, 100, -100> color rgb 1 }
light_source { <-50, 100, -50> color rgb 0.5 }

plane {
  y, 0
  pigment { checker Pink,Black scale 3 }
}


#macro Pump(offset_x)


  cylinder {
    <0, 0.2, 0>, <0, 14, 0>, 0.12
    pigment { color rgb<0.85, 0.85, 0.85> }
    finish { reflection 0.3 specular 0.9 roughness 0.02 }
    translate <offset_x, 0, 0>
  }


  cylinder {
    <0, 13.1, 0>, <0, 14.0, 0>, 0.65
    pigment { color rgb<0.75, 0.75, 0.75> }
    finish { reflection 0.3 specular 0.9 roughness 0.02 }
    translate <offset_x, 0, 0>
  }


  cylinder {
    <0, 14.0, 0>, <0, 15.8, 0>, 0.45
    pigment { color rgb<0.9, 0.9, 0.9> }
    finish { reflection 0.3 specular 0.9 roughness 0.02 }
    translate <offset_x, 0, 0>
  }


  cylinder {
    <0, 15.8, 0>, <0, 16.3, 0>, 0.6
    pigment { color rgb<0.95, 0.95, 0.95> }
    finish { reflection 0.2 specular 0.8 roughness 0.03 }
    translate <offset_x, 0, 0>
  }

  
  sphere {
    <0, 16.3, 0>, 0.6
    scale <1, 0.45, 1>
    pigment { color rgb<0.95, 0.95, 0.95> }
    finish { reflection 0.2 specular 0.8 roughness 0.03 }
    translate <offset_x, 0, 0>
  }


  cylinder {
    <0, 16.1, 0>, <1.1, 15.3, 0>, 0.18
    pigment { color rgb<0.8, 0.8, 0.8> }
    finish { reflection 0.3 specular 0.9 roughness 0.02 }
    translate <offset_x, 0, 0>
  }

 
  cylinder {
    <1.1, 15.3, 0>, <1.1, 14.6, 0>, 0.15
    pigment { color rgb<0.8, 0.8, 0.8> }
    finish { reflection 0.3 specular 0.9 roughness 0.02 }
    translate <offset_x, 0, 0>
  }

#end


#macro Bottle(offset_x, bottle_color)

  sor {
    13,
    <0.0,  0.0>,
    <1.2,   0.0>,
    <1.4,   0.5>,
    <1.6,   1.5>,
    <1.6,   5.5>,
    <1.5,   7.0>,
    <1.2,  8.0>,
    <0.9,  8.8>,
    <0.75,  9.5>,
    <0.75,  12.0>,
    <0.8,  12.5>,
    <0.7,  12.8>,
    <0.0,  13.1>
    open
    texture {
      pigment { color rgbt <1, 1, 1, 1> }
      finish {
        reflection { 0.15 }
        specular 0.85
        roughness 0.02
      }
    }
    translate <offset_x, 0, 0>
  }

  sor {
    8,
    <0.0,  0.1>,
    <1.08,   0.1>,
    <1.29,   0.6>,
    <1.49,   1.6>,
    <1.49,   3.8>,
    <1.39,   4.2>,
    <1.0,  5.0>,
    <0.0,  4.8>
    open
    texture {
      pigment { color bottle_color filter 0.8 }
      finish { diffuse 0.9 }
    }
    translate <offset_x, 0, 0>
  }

  Pump(offset_x)

#end


Bottle(0,  Yellow)
Bottle(5,  Brown)
Bottle(10, Turquoise)
Bottle(15, Violet)
