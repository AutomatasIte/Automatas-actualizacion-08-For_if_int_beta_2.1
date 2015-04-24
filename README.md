# Automatas-actualizacion-08-For_if_int_beta_2.1
#include <string.h>
#include <stdlib.h>
#include <stdio.h>


typedef struct
{
char c[30];
int token;
}asig_tok;
asig_tok atoken[]={
{"/",0},{"/=",1},
{".",2},{"..",3},
{"&",4},{"&=",5},{"&&",6},
{"|",7},{"|=",8},{"||",9},
{"-",10},{"-=",11},{"--",12},
{"+",13},{"+=",14},{"++",15},
{"<",16},{"<=",17},{"<<",18},{"<<=",19},
{"<>",20},{"<>=",21},
{">",22},{">=",23},{">>=",24},{">>>=",25},{">>",26},{">>>",27},
{"!",28},{"!=",29},{"!<>",30},{"!<>=",31},{"!<",32},{"!<=",33},{"!>",34},{"!>=",35},
{"(",36},{")",37},
{"[",38},{"]",39},
{"{",40},{"}",41},
{"?",42},
{",",43},{";",44},
{":",45},
{"$",46},
{"=",47},{"==",48},
{"*",49},{"*=",50},
{"%",51},{"%=",52},
{"^",53},{"^=",54},{"^^",55},
{"~",56},{"~=",57},
{"@",58},
{"=>",59},
{"#",60},
{"abstract",61},{"alias",62},{"aling",63},{"asm",64},{"assert",65},{"auto",66},
{"body",67},{"bool",68},{"break",69},{"byte",70},
{"case",71},{"cast",72},{"catch",73},{"cdouble",74},{"cent",75},{"cfloat",76},{"char",77},{"class",78},{"const",79},{"continue",80},{"creal",81},
{"dchar",82},{"debug",83},{"default",84},{"delegate",85},{"delete",86},{"deprecated",87},{"do",88},{"double",89},
{"else",90},{"enum",91},{"extern",92},{"esport",93},
{"false",94},{"final",95},{"finally",96},{"float",97},{"for",98},{"foreach",99},{"foreach_reverse",100},{"function",101},
{"goto",102},
{"if",103},{"ifloat",104},{"immutable",105},{"import",106},{"in",107},{"inout",108},{"int",109},{"interface",110},{"ireal",111},{"is",112},
{"long",113},
{"mixin",114},{"module",115},
{"new",116},{"null",117},
{"override",118},
{"package",119},{"pagmas",120},{"private",121},{"protected",122},{"public",123},{"pure",124},
{"real",125},{"ref",126},{"return",127},
{"shared",128},{"short",129},{"static if",130},{"struct",131},{"super",132},{"switch",133},
{"template",134},{"this",135},{"trow",136},{"true",137},{"try",138},{"typedef",139},{"typeid",140},{"typeof",141},
{"ubyte",142},{"ucent",143},{"uint",144},{"ulong",145},{"union",146},{"unittest",147},{"ushort",148},
{"version",149},{"void",150},
{"wchar",151},{"while",152},{"with",153},{"writeln",154},
{"Palabra Reservada",155},{"stdio",156},{"main",157},{"\"",158},{" ",159},{"\"",160},{"numero",1000}
};
///////////////////////////////////////////////////////////////////////////////////////////// creacion de la lista



struct node
    {
     char info[20];
     int linea;
     int ntoken;
     struct node *sig;
    };
    typedef struct node nodo;
    typedef nodo *tipolista;
    tipolista lista=NULL;



void crear(tipolista *lista,char x[30],int p,int u)
  {
     tipolista j, uri=*lista;
     j=(nodo*)malloc(sizeof(nodo));
     strcpy(j->info,x);
     j->linea=p;
     j->ntoken=u;
     j->sig=NULL;

     if(*lista==NULL)
     *lista=j;

     else
     { while(uri->sig!=NULL)
       uri=uri->sig;
       uri->sig=j;
     }
  }
   ///////////////////////////////////////////////////////////////////////////////////////////// creacion de la pila

typedef struct _nodo{
        int dato;
        char contenido[30];
        struct _nodo*sig;
        }tiponodo;
        
        typedef tiponodo *pnodo;
        typedef tiponodo *pila;
        
        
        void push(pila *pila, int v, char x[30])
        {
             pnodo nuevo;
             nuevo=(pnodo)malloc(sizeof(tiponodo));
             nuevo->dato=v;
             strcpy(nuevo->contenido,x);
             
             nuevo->sig=*pila;
             *pila=nuevo;
        }
        
        void pop(pila *pila)
        {
            pnodo nodo;
            int uri;
            nodo=*pila;
            
            if(!nodo)
            printf("no hay datos");
            
            if(nodo->dato!=36)
            printf("%s",nodo->contenido);
            
            *pila=nodo->sig;
            
            free(nodo);
            
        }
 /////////////////////////////////////////////////////////////// fin pila
  
  
  
//////////////////////////////////////////////// parea();inicio
int parea(int n)
   {
       if(n==lista->ntoken)
       {
       lista=lista->sig;
       return 1;
       }
      
       else
       {
        return 0;
       }
   }
   
   /////////////////////////////////posfija() inicio
void posfija()
{
  int extra=0; ///se incrementa cada vez que se analize un caracter de lalista
  int extra2=0;///este activador, detectar si ninguna if se a realizado este extra se mantendra en 0 y marcara un error debido a que el dato en la posfija no pertenece a una expresion matematica.
  int activador1=0; ////////se encarga de verificar los ()
  int activador2=0; ////////cuenta los operando
  int activador3=0; ////////se incrementa al encontrar un operador
  int activador4=1; //////// se encarga de dar fin ala posfija;
  pila pila=NULL;

       while(activador4!=0)
       {
            extra++;
            
            if(lista->ntoken==36||lista->ntoken==155)
            {
            extra2++;
              activador2=0;

                if(lista->ntoken==36)
                {
                activador1=1;
                push(&pila,lista->ntoken,lista->info);
                }
                
                if(lista->ntoken==155)
                {
                
                printf("%s",lista->info);
                }
                
                if(activador3==1)
                activador3++;
            }

            if(lista->ntoken==13||lista->ntoken==10||lista->ntoken==49||lista->ntoken==0)
            {
            extra2++;
                if(activador2==1)
                {
                    printf("error");
                    break;
                }
                 
                     push(&pila,lista->ntoken,lista->info);
                     activador2=1;
                     activador3++;
            } 
                 
             if(lista!=NULL)
             lista=lista->sig;
             
             if(extra==1&&activador2==1||extra2==0)
             {
             printf("error");
             break;
             }
           
           if(lista->ntoken==16||lista->ntoken==17||lista->ntoken==22||lista->ntoken==9||lista->ntoken==29||lista->ntoken==23||lista->ntoken==48||lista->ntoken==44||lista->ntoken==43||lista->ntoken==37||lista->ntoken==6)
           {/////if
                     
                     if(lista->ntoken!=37)
                     {
                         while(pila!=NULL)
                         {
                          pop(&pila);
                         }
                           
                           activador4=0;

                           if(activador1==1)
                           {
                           printf("error");
                           break;
                           }
                     }
                       
                     if(lista->ntoken==37)
                     {
                            if(activador1==1)
                            {
                                while(pila!=NULL)
                                {
                                 pop(&pila);
                                }
                              activador1=0;
                            }
                            else
                            {
                                while(pila!=NULL)
                                {
                                 pop(&pila);
                                }
                              activador4=0;
                            }
                     }

                    if(activador3==1||activador2==1)
                    {
                      printf("error con los operadores");
                      break;
                    }

             }////if
       }
}

  /////////////////////////////////posfija () fin 
   
   
   
   void imprimir(tipolista *p)
       {
         tipolista u;
         u=*p;
         
           while(u!=NULL)
           {
            printf("%s, %d ,%d \n",u->info,u->linea,u->ntoken);
            u=u->sig;
           }
       }
//////////////////////////////////////////////////funcion sencilla if
   void funcion_if()
   {
        int uri;
        uri=parea(36);
        
           while(lista->ntoken!=37||uri==0)
           {
               posfija();
               printf(" ");
        
                    if(lista->ntoken==22||lista->ntoken==23||lista->ntoken==16||lista->ntoken==17||lista->ntoken==29||lista->ntoken==48)
                    {
                        lista=lista->sig;
                    }
                    else
                    {
                        uri=0;
                        break;
                    }

                    posfija();
                    printf(" ");
               
                       if(lista->ntoken==6||lista->ntoken==9)
                       {
                          lista=lista->sig;
                       }
               
           }
       
        
           if(uri==1)
           printf(" \n si el if no menciona errores estas bien :) \n");
           else
           {
             printf("\n error en el if \n");
           }     
   }
//////////////////////////////////////////////////// funcion sencilla if  fin

void funcion_int()
{
     int ari=0;
     
     while(lista->ntoken!=44)
     {
         lista=lista->sig;
         
              if(lista->ntoken==155)
              {
                  lista=lista->sig;
              }
              else
              {
                printf("\n error en el int \n");
                break;
              }
     
                      if(lista->ntoken==44)
                      {
                        printf("\n correcto int \n");
                        break;
                      }
                      
                         if(lista->ntoken==47)
                         {
                                              lista=lista->sig;
                                              posfija();
                                              printf(" ");
                                              
                                              
                                                 if(lista->ntoken==44)
                                                 {
                                                   printf("\n correcto int \n");
                                                   break;                   
                                                 }
                                              
                         }
                         
                      if(lista->ntoken!=43)
                      {
                          printf("\n error en el int \n");
                          break;                  
                      }
     } //////////////////////////////////////int

} ///NOTA: SE ESTA MEJORANDO LA TABULACION :3 de poquito en poquito 

//////////////////////////////////////////funcion for
void funcion_for()
       {
            
            int a=0;  /// este contador se mantendra, al obtener un error se activara y al final nos indicara alguna falla en el for
            
            a=parea(36);
            a=parea(155); 
            a=parea(47);
            posfija(); 
            a=parea(44);
            a=parea(155);
            
               if(lista->ntoken==22||lista->ntoken==23||lista->ntoken==16||lista->ntoken==17||lista->ntoken==29||lista->ntoken==48)
               {
               lista=lista->sig; /// este if se mantendra igual
               }
               else
               {
               a=1;
               }
               
            posfija();
            a=parea(44);
            a=parea(155);
            
            if(lista->ntoken==47)
            {
                                 lista=lista->sig;
                                 posfija();
            }
            else
            {
                   if(lista->ntoken==12||lista->ntoken==15)           
                   lista=lista->sig;                       
                   else                                    
                   {                                       
                     a=0;                                 
                   }
            }
            
            a=parea(37);
               
            if(a==0)
            printf("error en el for declarado \n"); // al final si se presento un error el contador sera mayor a 0 de lo contrario este sera correcto
            else
            {
                printf("correcto tu for \n");
            }
       }


///////////////////////////////////////////funcion for fin


  int main()
       {//////////////inicio
         printf("\n PROGRAMA QUE ABRE UN ARCHIVO DE TEXTO \n");

         FILE* miarchivo=NULL;
         char* nombrearchivo="prueba.txt";
         char fila;
         char cadena[50];
         int u=0;
         int linea=0;
         int i,z,uri=0;
         miarchivo=fopen(nombrearchivo,"r");
         

         while(feof(miarchivo)==0){ ////INICIO DEL WHILE
         fila=fgetc(miarchivo);
         uri=0;


         if(fila!='\n')
         {
             if(fila!=' ')
             {
              cadena[u]=fila;
              u++;
             }
         }


         if((fila==' ')||(fila=='\n'))
         {   /////////////uno inicio
           cadena[u]='\0';
           for(i=0;i<162;i++)
           {
            if(strcmp(cadena,atoken[i].c)==0)
           {
           z=atoken[i].token;
           uri=1;
           }
         }

         if(uri==0)
         {
          z=155; /////// con 155 me refiero a que es una palabra normal
         }

         crear(&lista,cadena,linea,z);
         u=0;
         free(cadena);
         }

         if(fila=='\n')
         linea++;

         }

          fclose(miarchivo);
    ///////////////////////////////////////////////////////////////separador      
          imprimir(&lista);
          
          
          while(lista!=NULL)
          {
                        
                if(lista->ntoken==103)
                {
                  ///imprimir(&lista);
                  printf("\n");
                  lista=lista->sig;         
                 funcion_if();                            
                }
           
                       if(lista->ntoken==109)
                        {
                          ///imprimir(&lista);
                          funcion_int();
                        }
                        
                             if(lista->ntoken==98)
                               {                    
                                 lista=lista->sig;
                                 funcion_for();
                               } 
           
                       if(lista!=NULL)
                       lista=lista->sig;
          
          }//////////////////////////////// FIN IF
        
        
        
          printf("\n \n");
          system("PAUSE");
          return 0;
         }/////////fin
