#include <stdio.h>
#include <stdlib.h>


/* run this program using the console pauser or add your own getch, system("pause") or input loop */


int troca = 0;
int comparacao = 0;

void selectionSort(int vetor[], int tam) {

 int i, j, min, aux;

 for (i = 0; i < (tam-1); i++) {
 	
 comparacao++;	

 min = i;

 for (j = (i+1); j < tam; j++) {


 troca ++;

 if (vetor[j] < vetor[min]) {

 min = j;

 }

 }

 if (i != min) {

 aux = vetor[i];

 vetor[i] = vetor[min];

 vetor[min] = aux;

 }

 }

}

void insertionSort(int vetor[], int tam){

 int j,i,key;

 for(j = 1; j < tam; j++){

 key = vetor[j];

 //i = j – 1;

 while(i >= 0 && vetor[i] > key){

 vetor[i + 1] = vetor[i];

 //i = i – 1;

 }

 vetor[i + 1] = key;

 }

}

void quickSort(int vetor[], int esquerda, int direita) {

 //onde esquerda aponta o início do vetor e direita o final do vetor

 int i, j, x, y;

 i = esquerda;

 j = direita;

 x = vetor[(esquerda + direita) / 2];

 while(i <= j)

 { while(vetor[i] < x && i < direita)

 { i++; }

 while(vetor[j] > x && j > esquerda)

 { j--; }

 if(i <= j)

 { y = vetor[i];

 vetor[i] = vetor[j];

 vetor[j] = y;

 i++;

 j--;

 }

 }

 if(j > esquerda) { quickSort(vetor, esquerda, j); }

 if(i < direita) { quickSort(vetor, i, direita); }

}


void merge(int vetor[], int tam) {

 int mid;

 int i, j, k;

 int* tmp;

 tmp = (int*) malloc(tam * sizeof(int));

 if (tmp == NULL) { exit(1); }

 mid = tam / 2;

 i = 0;

 j = mid;

 k = 0;

 while (i < mid && j < tam) {

 if (vetor[i] <= vetor[j]) { tmp[k] = vetor[i++]; }

 else { tmp[k] = vetor[j++]; }

 ++k;

 }

 if (i == mid) {

 while (j < tam) { tmp[k++] = vetor[j++]; }

 } else {

 while (i < mid) { tmp[k++] = vetor[i++]; }

 }

 for (i = 0; i < tam; ++i) {

 vetor[i] = tmp[i]; }

 free(tmp);

}

void mergeSort(int vetor[], int tam) {

 int mid;

 if (tam > 1) {

 mid = tam / 2;

 mergeSort(vetor, mid);

 mergeSort(vetor + mid, tam - mid);

 merge(vetor, tam);

 }

}


void shellSort(int *vetor, int tam) {

 int i , j , value;

 int gap = 1;

 while (gap < tam) { gap = 3*gap+1; }

 while (gap > 1) {

 gap /= 3;

 for(i = gap; i < tam; i++) {

 value = vetor[i];

 j = i - gap;

 while (j >= 0 && value < vetor[j]) {

 vetor[j + gap] = vetor[j];

 j -= gap;

 }

 vetor[j + gap] = value;

 }

 }

}


void heapSort(int vetor[], int tam)

{ int i = tam/2, pai, filho, t;

 for (;;)

 { if (i > 0)

 { i--;

 t = vetor[i]; }

 else

 { tam--;

 if (tam == 0) { return; }

 t = vetor[tam];

 vetor[tam] = vetor[0]; }

 pai = i;

 filho = i*2; //Será feita a comparação com o filho da esquerda.

 while (filho < tam)

 { //Se o filho da esquerda for menor do que o filho da direita,

 //então será feita a troca do filho que será comparado.

 if ((filho + 1 < tam) && (vetor[filho + 1] > vetor[filho]))

 { filho++; }

 if (vetor[filho] > t)

 { vetor[pai] = vetor[filho];

 pai = filho;

 filho = pai*2 + 1;

 } else { break; }

 } vetor[pai] = t;

 }

}


void imprimirVetor(int vetor[],int tam){
	
	int i ;
   	
	for(i=0; i<tam; i++){
		
		
		printf("%d",vetor[i]);	
		printf("\n");
		
	}
	
	
	
}

void criarVetor(int tamanho){


	
}


int main(int argc, char *argv[]) {
	
	int vetor[8] = {6,3,5,1,8,2,4,7};
	int tam = 8;
	int tipoOrder;
	
	
	//printf("\n\n Nao Ordenado\n\n");  -- Imprimindo valores não ordenados
	//imprimirVetor(vetor,tam);
	 	
	printf(" SelectSort    digite 1 \n\n ");
	printf("InsertionSort digite 2 \n\n ");
	printf("QuickSort     digite 3 \n\n ");
	printf("MergeSort     digite 4 \n\n ");
	printf("ShellSort     digite 5 \n\n ");
	printf("HeapSort      digite 6 \n\n ");
	
	
	printf("Digite o Tipo de OrdenaCao: ");
	scanf("%d",&tipoOrder);

    switch (tipoOrder){
    	
    	case 1 :
    	
    	selectionSort(vetor,tam);
    	
    	break;
    	
    	//case 2 :
    	
    	//insertionSort(vetor, tam); -- Problemas	
    	
    	//break;
    	
    	//case 3 :
    	
    	//quickSort(vetor, tam);  -- Problemas	
    	
    	//break;
    	
    	case 4 :
    		
    	merge(vetor, tam);	
    	mergeSort(vetor, tam);	
    	
    	break;
    	
       	case 5 :
    	
    	shellSort(vetor, tam);	
    	
    	break;
    	
      	case 6 :
    	
    	heapSort(vetor, tam);	
    	
    	break;
    	
    	
    	
	}

	printf("\n\n Ordenado\n\n");
	imprimirVetor(vetor,tam);
	
	
    printf("\n\n Numero de trocas : ");	
   	printf("\n\n %d \n\n",troca);
   	printf("\n\n Numero de comparacao : ");	
	printf("\n\n %d \n\n",comparacao);   	
   	printf("\n\n ");
   	
   	
   	
	
	
	return 0;
}
