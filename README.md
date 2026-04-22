#include "colors.inc"
#include "textures.inc" 
 camera {
   location <1, 10, -35>
   look_at <8, 6.5, 0>
 }

 light_source { <-3, 10, -3> White  }
 light_source { <20, 10, -3> White  }
 background{ NeonBlue}           //Öâåò ôîíà ,à òî÷íåå íåáà íà ðèñóíêå  
 
 
 plane{ y,-10
          pigment { checker Pink,Black scale 3 }
 }
 //Ïîñòðîåíèå ïàðàëëåëåïèïåäà. 
#declare stool=union{
 box { <0, 0, 0>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      < 21, 0.5, 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
 }
                                
}

#declare skaf=union{
 object{
    stool
 }

 object{
    stool
 translate<0,-9,0>
}

 object{
    stool
 translate<0,-4.5,0>
}

 object{
    stool
    translate<0,18,0>
}
 object{
    stool
    translate<0,22,0>
}
                    
} 
 object{
    skaf
}
#declare boc=union{
    box { <0, 0, -0.1>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
          < 6.9, -10, -0.1>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
          texture {                  
             pigment { wood } //color White -çàêðàñèòü â áåëûé öâåò 
          }
    }
}

object{
    boc
}
object{
    boc
    translate<7,0,0>
}

object{
    boc
    translate<14,0,0>
}

//bok nis

#declare boknis=union{
 box { <0, 0, 0>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      < 0,-10 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
 }
                                
}

object{
 boknis
}
object{
 boknis
 translate<21,0,0>
}

//stenka sadi

box { <0, 22, 13>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      < 21,-10 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { wood } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
 } 
 
// bok verh

#declare bokverh=union{
 box { <0, 18, 0>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      < 0, 22 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
 }
                                
}

object{
 bokverh                            
}
object{
 bokverh
 translate<21,0,0>
}

// stenka verh pered

box { <0, 18, 0>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      < 21, 22 , 0>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
 } 
 
// sredni ogroshdenie 

box { <11, 0, 1.5>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      < 14, 18 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
 } 


 
// kvadrat nad avtomatom

box { <14, 12, 1.5>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      < 21, 18 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
 }
 
// polki vse 

box { <0, 0, 11>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      < 0.4, 18 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
}
#declare bo=union{ 
box { <0.5, 0, 11>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      <0.9 , 16 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
    }
}
object{
 bo                            
}
object{
 bo
 translate<10,0,0>
}
object{
 bo
 translate<5,0,0>
}
  
#declare bov=union{
box { <0.5, 15.6, 11>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      <10.9 , 16 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
    }
}
object{
 bov                            
}
object{
 bov
 translate<0,-15.1,0>
} 
object{
 bov
 translate<0,-6.5,0>
}
object{
 bov
 translate<0,-9,0>
}

#declare boz=union{ 
box { <2.9, 0.2, 11>,                //Íèæíèé áëèæíèé ëåâûé óãîë 
      <3.3 , 7 , 13>               //Äàëüíèé âåðõíèé ïðàâûé óãîë
      texture {                  
         pigment { color Gray35 } //color White -çàêðàñèòü â áåëûé öâåò 
      }                          
    }
}
object{
 boz                            
}
object{
 boz
 translate<5,9,0>
}
object{
 boz
 translate<5,0,0>
}
object{
 boz
 translate<0,9,0>
}   
cylinder{<12.5, 13,2>,<12.5,  13, 1>, 1.1 pigment {Grey filter 0.2} finish{diffuse 1}}    //ýòî ãäå ëåæàò ñòàêàí÷èêè 
cylinder{<12.5, 15.5,2>,<12.5,  15.5, 1>, 1.1 pigment {Grey}}  
cylinder{<12.5, 13,1>,<12.5,  13, 0>, 0.6 pigment {Red}}
cylinder{<12.5, 15.5,1>,<12.5,  15.5,0>, 0.6 pigment {Red}}      
cylinder{<12.5, 13,1>,<12.5,  13, -0.2>, 0.4 pigment {White}}
cylinder{<12.5, 15.5,1>,<12.5,  15.5,-0.2>, 0.4 pigment {White}} 
cylinder{<14.7, -0.8,1>,<14.7, -0.8,-0.2>, 0.2 pigment {White}}  //ðó÷êè çàìîê    
cylinder{<5.9, -0.8,1>,<5.9, -0.8,-0.2>, 0.2 pigment {White}}
cylinder{<7.7, -0.8,1>,<7.7, -0.8,-0.2>, 0.2 pigment {White}}        

sor {
    12,
    <1,  -0.1>,
    <0.8,  1>,
    <0.8,  2>,
    <0.8,  2.5>,
    <0.8,  3>,
    <0.8,  3.5>,
    <0.8, 3.6>,
    <0.8, 3.8>,
    <0.3, 5.9>,
    <0.3, 6.4>,
    <0.1, 7>,
    <0.1, 7> 
    open 
    texture {Glass}
  }


    

