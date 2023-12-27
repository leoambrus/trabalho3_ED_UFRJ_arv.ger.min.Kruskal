#include <stdio.h>

struct aresta {
    int A1;
    int A2;
    int peso;
};

int ciclo[1000];  // Vetor que representa os conjuntos disjuntos (Union-Find)

void unir(int A1, int A2);  // Função para unir dois conjuntos
int pai(int x);  // Função para encontrar o representante (pai) de um conjunto
void countSort(struct aresta *A, int tamanhoVetor, int k);  // Algoritmo de Counting Sort

int main() {
    int n;
    scanf("%d", &n);

    struct aresta arestas[1000];  // Supondo um máximo de 100 arestas

    // Inicialização dos conjuntos disjuntos
    int i = 0;
    while (i < n) {
        ciclo[i] = i;
        i++;
    }

    int m = 0;  // Variável para contar o número de arestas inseridas

    // Entrada das arestas do grafo usando EOF para encerrar
    while (scanf("%d %d %d", &arestas[m].A1, &arestas[m].A2, &arestas[m].peso) != EOF) {
        m++;
    }

    int pesoTotal = 0;  // Variável para armazenar o peso total da MST

    // Encontre o valor máximo de peso para usar no Count Sort
    int maxPeso = 0;
    i = 0;
    while (i < m) {
        if (arestas[i].peso > maxPeso) {
            maxPeso = arestas[i].peso;
        }
        i++;
    }

    // Ordenação das arestas pelo peso usando o Counting Sort
    countSort(arestas, m, maxPeso);

    // Construção da MST usando o algoritmo de Kruskal
    i = 0;
    while (i < m) {
        // Verifica se as extremidades pertencem ao mesmo conjunto
        if (pai(arestas[i].A1) != pai(arestas[i].A2)) {
            pesoTotal += arestas[i].peso;  // Adiciona o peso da aresta à MST
            unir(arestas[i].A1, arestas[i].A2);  // Realiza a união dos conjuntos
        }
        i++;
    }

    printf("%d\n", pesoTotal);  // Imprime o peso total da MST

    return 0;
}

void unir(int A1, int A2) {
    ciclo[pai(A1)] = pai(A2);  // Faz a união atualizando o pai do conjunto de A1 para o pai de A2
}

int pai(int v) {
    if (ciclo[v] == v) {
        return v;  // Se v é o representante (pai) do conjunto, retorna v
    }

    ciclo[v] = pai(ciclo[v]);  // Atualiza o pai para otimizar futuras chamadas
    return ciclo[v];
}

void countSort(struct aresta *A, int tamanhoVetor, int k) {
    int count[k + 1];

    // Inicialização do array count
    int i = 0;
    while (i < k + 1) {
        count[i] = 0;
        i++;
    }

    // Contagem de ocorrências de cada peso
    i = 0;
    while (i < tamanhoVetor) {
        count[A[i].peso]++;
        i++;
    }

    int j = 0;
    // Atualização do vetor de arestas ordenado
    i = 0;
    while (i <= k) {
        while (count[i] > 0) {
            A[j].peso = i;
            j++;
            count[i]--;
        }
        i++;
    }
}
