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

plane { y, -10 pigment { checker Pink, Black scale 3 } }

// Построение параллелепипеда
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

// Стенка сзади
box { <0, 22, 13>, <21, -10, 13> texture { pigment { wood } } }

#declare bokverh = union {
  box { <0, 18, 0>, <0, 22, 13> texture { pigment { color Gray35 } } }
}
object { bokverh }
object { bokverh translate <21, 0, 0> }

// Стенка верхняя передняя
box { <0, 18, 0>, <21, 22, 0> texture { pigment { color Gray35 } } }

// Среднее ограждение
box { <11, 0, 1.5>, <14, 18, 13> texture { pigment { color Gray35 } } }

// Квадрат над автоматом
box { <14, 12, 1.5>, <21, 18, 13> texture { pigment { color Gray35 } } }

// Полки
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
// Ставим их на столешницу (Y = 0.5) справа от кофемашины
Bottle(22.0, Yellow, 0.5)
Bottle(24.0, Brown, 0.5)
Bottle(26.0, Turquoise, 0.5)
Bottle(28.0, Violet, 0.5)
