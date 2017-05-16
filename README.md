#include<stdio.h>
#include<stdlib.h>



int main()
{
    int m, n, i, j, **Arr = NULL, d, **Arr4 = NULL;
    float **Arr2 = NULL, *Arr3 = NULL;
    
    printf("\nEnter n and m\nn = ");
    scanf("%i", &n);
    printf("m = ");
    scanf("%i", &m);
    
    //Выделение памяти и заполнение массива случайными числами
    
    Arr = (int**)malloc(n * sizeof(int*));

    for(i = 0; i < n; i++)
    {
        Arr[i] = (int*)malloc(m * sizeof(int));
    }
    for(i = 0; i < n; i++)
    {
        printf("\n");
        for(j = 0; j < m; j++)
        {
            Arr[i][j] = ((rand() % (20 * 2) + 1) - 20);
            printf("%i ", Arr[i][j]);
        }
    }
    //Задание номер 1.
    printf("\n\nTask 1.\nSum = %i\n\n", decision1(Arr, m , n));
    //Задание номер 2.
    printf("Task 2.");
    printf("\nMin = %i", decision2(Arr, n, m));
    //Задание номер 3.
    printf("\n\nTask 3.");
    Arr2 = (float**)malloc(n * sizeof(float*));

    for(i = 0; i < n; i++)
    {
        Arr2[i] = (float*)malloc(m * sizeof(float));
    }
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < n; j++)
        {
            Arr2[i][j] = ((rand() % (20 * 2) + 1) - 20);
        }
    }
    d = n * 2;
    Arr3 = (float*)malloc(n * sizeof(float));
    for(i = 0; i < n; i++)
    {
        printf("\n");
        for(j = 0; j < n; j++)
        {
            printf("%0.1f ", Arr2[i][j]/decision3(Arr2, Arr3 ,n));
        }
    }
    //Задание 4
    printf("\n\nTask 4.");
    Arr4 = (int**)malloc(m * sizeof(int*));

    for(i = 0; i < n; i++){
        Arr4[i] = (int*)malloc(n * sizeof(int));
    }
    decision4(Arr, Arr4 ,n, m);
    free(Arr);
    free(Arr2);
    free(Arr3);
    free(Arr4);
    return 0;
}





//Задание 1.Нахождение суммы в тех столбцах которые имеют только положительные элементы
int decision1(int **Arr, int m, int n)
{
    int i = 0, x , j, sum = 0;
    do
    {
        x = 0;
        for(j = 0; j < m; j++)
        {
            if(Arr[i][j] > 0)
            {
                x++;
            }
        }
        if(x == n)
        {
            for(j = 0; j < m; j++)
            {
                sum = sum + Arr[i][j];
            }
        }
        i++;
    }while(i < n);
    
    return sum;
}
//Задание номер 2. 
int decision2(int **Arr, int n, int m)
{
    int i, j, firstSum = 0, secondSum = 0, min;
    
    for(i = n - 2, j = 0; i >= 0; i--, j++){
        firstSum = firstSum + abs(Arr[i][j]);
    }

    for(i = n - 1, j = 1; j < m; i--, j++){
        secondSum = secondSum + abs(Arr[i][j]);
    }
    
    if(firstSum > secondSum){
        min = secondSum;
    }
    else{
        min = firstSum;
    }
    
    return min;
}

int decision3(float **Arr2, float *Arr3, int n){
    int i, j, sum = 0;
    for(i = 0; i < n; i++){
            Arr3[i] = Arr2[i][i];
        }
    for(i = n - 1, j = 0; i > -1; i--, j++, n++){
        Arr3[n] = Arr2[i][j];
    }
    for(i = 0; i < n ; i++){
        sum += Arr3[i];
    }
    
    return sum;
}

void decision4(int **Arr, int **Arr4, int n, int m){
    int i, j;
    
    for(i = 0; i < n; i++){
        printf("\n");
        for(j = 0; j < m; j++){
            Arr4[i][j] = Arr[j][i];
            printf("%i ", Arr4[i][j]);
        }
    }
}
