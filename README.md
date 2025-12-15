# School21


#include <stdio.h>
#define NMAX 10

int input(int *buffer, int *length);
void output(int sum, int *buffer, int length);
int sum_numbers(int *buffer, int length);
int find_numbers(int *buffer, int length, int *numbers, int number);

int main() {
  int rows1, data[NMAX];
  int rows2 = 0, final_data[NMAX];
  if (input(data, &rows1) == 1) {
    printf("n/a");
    return 1;
  }

  rows2 = find_numbers(data, rows1, final_data, rows2);
  if (rows2 == 0) {
    printf("n/a");
    return 1;
  }

  // Выводим сумму и новый массив
  output(sum_numbers(data, rows1), final_data, rows2);

  return 0;
}

int input(int *data, int *n) {
  char c;
  if (scanf("%d", n) != 1 || *n <= 0 || *n > NMAX || scanf("%c", &c) != 1 ||
      c != '\n')
    return 1;

  for (int *p = data; p - data < *n; p++) {
    if (scanf("%d", p) != 1)
      return 1;
  }

  c = 0;
  if (scanf("%c", &c) != 0 && c != '\n')
    return 1;
  return 0;
}

void output(int sum, int *data, int n) {
  printf("%d\n", sum);
  for (int *p = data; p - data < n; p++) {
    printf("%d", *p);
    if (p - data != n - 1)
      printf(" ");
  }
}

/*------------------------------------
    Функция находит сумму четных элементов
-------------------------------------*/
int sum_numbers(int *buffer, int length) {
  int sum = 0;

  for (int i = 0; i < length; i++) {
    if (buffer[i] % 2 == 0) {
      sum += buffer[i];
    }
  }
  return sum;
}

/*------------------------------------
    Функция находит все элементы, НА КОТОРЫЕ
    делится нацело сумма четных чисел
    (т.е. сумма % элемент == 0)
-------------------------------------*/
int find_numbers(int *buffer, int length, int *numbers, int number) {
  int sum = sum_numbers(buffer, length);

  // Если сумма 0, то она делится на все числа (кроме 0)
  // Но обычно 0 делится на любое число (0 % x == 0)
  for (int i = 0; i < length; i++) {
    // Элемент не должен быть 0 (деление на 0)
    if (buffer[i] != 0 && sum % buffer[i] == 0) {
      numbers[number] = buffer[i];
      number++;
    }
  }
  return number;
}
