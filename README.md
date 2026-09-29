# Tarefas-C

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int comparar(const void *a, const void *b) {
    double x = *(const double *)a;
    double y = *(const double *)b;
    return (x > y) - (x < y);
}

int main(void) {
    int n;

    if (scanf("%d", &n) != 1 || n <= 0) {
        return 1;
    }

    double *valores = malloc(n * sizeof(double));
    if (valores == NULL) {
        return 1;
    }

    double soma = 0.0;
    for (int i = 0; i < n; i++) {
        if (scanf("%lf", &valores[i]) != 1) {
            free(valores);
            return 1;
        }
        soma += valores[i];
    }

    double media = soma / n;

    double acumulado = 0.0;
    for (int i = 0; i < n; i++) {
        double d = valores[i] - media;
        acumulado += d * d;
    }
    double desvio = sqrt(acumulado / n);

    qsort(valores, n, sizeof(double), comparar);

    double mediana;
    if (n % 2 == 1) {
        mediana = valores[n / 2];
    } else {
        mediana = (valores[n / 2 - 1] + valores[n / 2]) / 2.0;
    }

    printf("Maximo: %.2f\n", valores[n - 1]);
    printf("Minimo: %.2f\n", valores[0]);
    printf("Media: %.2f\n", media);
    printf("Mediana: %.2f\n", mediana);
    printf("Desvio-padrao: %.2f\n", desvio);

    free(valores);
    return 0;
}
