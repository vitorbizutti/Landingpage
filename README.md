# Landingpage





#include <stdio.h>
#include <stdlib.h>
#include <math.h>

void aloca(int **p, int tam);
void leitura(int *p);
void imprime(int *p, int tam);
int impar(int *p, int tam, int **pI);

main()
{
int cont=0,qImpar=0,soma=0;
int *ptr=NULL,*pImpar=NULL;
char op;

do{
aloca(&ptr,cont+1);
leitura(ptr+cont);
cont++;
printf("\nDeseja continuar <S/N>?: ");
scanf("%c",&op);
fflush(stdin);
}while(op!= 'N' && op!= 'n');

printf("\nNumeros digitados: ");
imprime(ptr,cont);

qImpar=impar(ptr,cont,&pImpar);
printf("\nNumeros impares: ");
imprime(pImpar,qImpar);
}

void aloca(int **p, int tam)
{
if((*p=(int *)realloc(*p,tam*sizeof(int)))==NULL)
exit(1);
}

void leitura(int *p)
{
printf("\nDigite um numero: ");
scanf("%i",p);
fflush(stdin);
}

void imprime(int *p, int tam)
{
int i;

for(i=0;i<tam;i++)
printf("\n%.2i",*(p+i));
}

int impar(int *p, int tam, int **pI)
{
int i,qI=0,soma,aux;
aux=tam;

if(tam % 2 == 0)
{
tam= tam/2;
for(i=0;i<tam;i++,aux--)
{
soma=*(p+i)+*(p+aux);
if((soma % 2) == 1)
{
aloca(pI,qI+1);
*(*pI+qI)=soma;
qI++;
}
}
}
else
{
tam=(tam-1)/2;
for(i=0;i<tam;i++,aux--)
{
soma=*(p+i)+*(p+aux);
if((soma % 2) == 1)
{
aloca(pI,qI+1);
*(*pI+qI)=soma;
qI++;
}
}
aux=(aux/2)-0,5;
if((*(p+aux) % 2) == 1)
{
aloca(pI,qI+1);
*(*pI+qI)=*(p+aux);
qI++;
}
}
return qI;
}