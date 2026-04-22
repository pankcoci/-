#include "colors.inc"
#include "textures.inc"
#include "but.pov"

camera {
  location <1, 10, -35>
  look_at <8, 6.5, 0>
}

light_source { <-3, 10, -3> White }
light_source { <20, 10, -3> White }
background { NeonBlue }

// Пол
plane { y, -10 pigment { checker Pink, Black scale 3 } }

// ========== КОФЕМАШИНА (твой код) ==========

#declare stool = union {
  box { <0, 0, 0>, <21, 0.5, 13> texture { pigment { color Gray35 } } }
}

#declare skaf = union {
  object { stool }
  object { stool translate <0, -9, 0> }
  object { stool translate <0, -4.5, 0> }
  object { stool translate <0, 18, 0> }
  object { stool translate <0, 22, 0> }
}
object { skaf }

#declare boc = union {
  box { <0, 0, -0.1>, <6.9, -10, -0.1> texture { pigment { wood } } }
}
object { boc }
object { boc translate <7, 0, 0> }
object { boc translate <14, 0, 0> }

#declare boknis = union {
  box { <0, 0, 0>, <0, -10, 13> texture { pigment { color Gray35 } } }
}
object { boknis }
object { boknis translate <21, 0, 0> }

box { <0, 22, 13>, <21, -10, 13> texture { pigment { wood } } }

#declare bokverh = union {
  box { <0, 18, 0>, <0, 22, 13> texture { pigment { color Gray35 } } }
}
object { bokverh }
object { bokverh translate <21, 0, 0> }

box { <0, 18, 0>, <21, 22, 0> texture { pigment { color Gray35 } } }
box { <11, 0, 1.5>, <14, 18, 13> texture { pigment { color Gray35 } } }
box { <14, 12, 1.5>, <21, 18, 13> texture { pigment { color Gray35 } } }
box { <0, 0, 11>, <0.4, 18, 13> texture { pigment { color Gray35 } } }

#declare bo = union {
  box { <0.5, 0, 11>, <0.9, 16, 13> texture { pigment { color Gray35 } } }
}
object { bo }
object { bo translate <10, 0, 0> }
object { bo translate <5, 0, 0> }

#declare bov = union {
  box { <0.5, 15.6, 11>, <10.9, 16, 13> texture { pigment { color Gray35 } } }
}
object { bov }
object { bov translate <0, -15.1, 0> }
object { bov translate <0, -6.5, 0> }
object { bov translate <0, -9, 0> }

#declare boz = union {
  box { <2.9, 0.2, 11>, <3.3, 7, 13> texture { pigment { color Gray35 } } }
}
object { boz }
object { boz translate <5, 9, 0> }
object { boz translate <5, 0, 0> }
object { boz translate <0, 9, 0> }

// Стаканы
cylinder { <12.5, 13, 2>, <12.5, 13, 1>, 1.1 pigment { Grey filter 0.2 } finish { diffuse 1 } }
cylinder { <12.5, 15.5, 2>, <12.5, 15.5, 1>, 1.1 pigment { Grey } }
cylinder { <12.5, 13, 1>, <12.5, 13, 0>, 0.6 pigment { Red } }
cylinder { <12.5, 15.5, 1>, <12.5, 15.5, 0>, 0.6 pigment { Red } }
cylinder { <12.5, 13, 1>, <12.5, 13, -0.2>, 0.4 pigment { White } }
cylinder { <12.5, 15.5, 1>, <12.5, 15.5, -0.2>, 0.4 pigment { White } }
cylinder { <14.7, -0.8, 1>, <14.7, -0.8, -0.2>, 0.2 pigment { White } }
cylinder { <5.9, -0.8, 1>, <5.9, -0.8, -0.2>, 0.2 pigment { White } }
cylinder { <7.7, -0.8, 1>, <7.7, -0.8, -0.2>, 0.2 pigment { White } }

sor {
  12,
  <1, -0.1>, <0.8, 1>, <0.8, 2>, <0.8, 2.5>, <0.8, 3>,
  <0.8, 3.5>, <0.8, 3.6>, <0.8, 3.8>, <0.3, 5.9>, <0.3, 6.4>, <0.1, 7>, <0.1, 7>
  open texture { Glass }
}

// ========== БУТЫЛКИ из but.pov ==========
// Поднимаем их на уровень столешницы (Y = 0.5) и ставим справа от кофемашины (X от 22 до 28)

#macro Pump(offset_x, y_level)
  cylinder { <0, 0.2, 0>, <0, 14, 0>, 0.12 pigment { color rgb<0.85,0.85,0.85> } finish { reflection 0.3 specular 0.9 roughness 0.02 } scale 0.35 translate <offset_x, y_level, 9> }
  cylinder { <0, 13.1, 0>, <0, 14.0, 0>, 0.65 pigment { color rgb<0.75,0.75,0.75> } finish { reflection 0.3 specular 0.9 roughness 0.02 } scale 0.35 translate <offset_x, y_level, 9> }
  cylinder { <0, 14.0, 0>, <0, 15.8, 0>, 0.45 pigment { color rgb<0.9,0.9,0.9> } finish { reflection 0.3 specular 0.9 roughness 0.02 } scale 0.35 translate <offset_x, y_level, 9> }
  cylinder { <0, 15.8, 0>, <0, 16.3, 0>, 0.6 pigment { color rgb<0.95,0.95,0.95> } finish { reflection 0.2 specular 0.8 roughness 0.03 } scale 0.35 translate <offset_x, y_level, 9> }
  sphere { <0, 16.3, 0>, 0.6 scale <1,0.45,1> pigment { color rgb<0.95,0.95,0.95> } finish { reflection 0.2 specular 0.8 roughness 0.03 } scale 0.35 translate <offset_x, y_level, 9> }
  cylinder { <0, 16.1, 0>, <1.1, 15.3, 0>, 0.18 pigment { color rgb<0.8,0.8,0.8> } finish { reflection 0.3 specular 0.9 roughness 0.02 } scale 0.35 translate <offset_x, y_level, 9> }
  cylinder { <1.1, 15.3, 0>, <1.1, 14.6, 0>, 0.15 pigment { color rgb<0.8,0.8,0.8> } finish { reflection 0.3 specular 0.9 roughness 0.02 } scale 0.35 translate <offset_x, y_level, 9> }
#end

#macro Bottle(offset_x, bottle_color, y_level)
  sor {
    13,
    <0.0,0.0>, <1.2,0.0>, <1.4,0.5>, <1.6,1.5>, <1.6,5.5>,
    <1.5,7.0>, <1.2,8.0>, <0.9,8.8>, <0.75,9.5>, <0.75,12.0>,
    <0.8,12.5>, <0.7,12.8>, <0.0,13.1>
    open
    texture { pigment { color rgbt <1,1,1,1> } finish { reflection 0.15 specular 0.85 roughness 0.02 } }
    scale 0.35
    translate <offset_x, y_level, 9>
  }
  sor {
    8,
    <0.0,0.1>, <1.08,0.1>, <1.29,0.6>, <1.49,1.6>, <1.49,3.8>,
    <1.39,4.2>, <1.0,5.0>, <0.0,4.8>
    open
    texture { pigment { color bottle_color filter 0.8 } finish { diffuse 0.9 } }
    scale 0.35
    translate <offset_x, y_level, 9>
  }
  Pump(offset_x, y_level)
#end

// Ставим бутылки справа от кофемашины (X от 22 до 28) на высоте Y = 0.5 (столешница)
Bottle(22.0, Yellow, 0.5)
Bottle(24.0, Brown, 0.5)
Bottle(26.0, Turquoise, 0.5)
Bottle(28.0, Violet, 0.5)
