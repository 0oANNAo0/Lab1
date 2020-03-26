# Lab1
Lab1 VIPZ
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct book {
  char author[255];
  char title[255];
  int year;
  int pages;
  double price;
  struct book* next;
} Book;

int main() {
  FILE* file = fopen("dat.txt", "r");
  Book* head = NULL;
  Book* current = NULL;
  while(!feof(file)) {
    Book* book = (Book*) calloc(1, sizeof(Book));
    fscanf(file, "%s%s%d%d%lf", book->author, book->title, &book->year, &book->pages, &book->price);
    if(strlen(book->title) == 0) {
      free(book);
      continue;
    }
    if(head == NULL) {
      head = book;
      current = head;
    } else {
      current->next = book;
      current = book;
    }
    printf("Book \"%s\" by %s, %d year, %d pages, $%lf\n", book->title, book->author, book->year, book->pages, book->price);
  }

  printf("Enter book to insert:\n");
  Book* book = (Book*) calloc(1, sizeof(Book));
  scanf("%s%s%d%d%lf", book->author, book->title, &book->year, &book->pages, &book->price);
  printf("%s\n", book->author);
  // insert to list
  current->next = book;
  current = book;

  printf("Books witch sarted with D\n");
  // remove from list
  current = head;
  Book* prev = NULL;
  while(current != NULL) {
    Book* book = current;
    if(book->title[0] == 'd' || book->title[0] == 'D') {
      if(book == head) {
        head = book->next;
      } else {
        prev->next = book->next;
      }
    } else {
      printf("Book \"%s\" by %s, %d year, %d pages, $%lf\n", book->title, book->author, book->year, book->pages, book->price);
      prev = current;
    }
    current = current->next;
    
  }

  return 0;
}
