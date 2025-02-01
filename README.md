# compiler_design
   #include<stdio.h>
   #include<stdlib.h>
   #include<string.h>
   #include<ctype.h>
  const char *keywords[] = {"int", "float", "if", "else", "while", "for", "return", "char", "void", "double"};
   const int keywordcount = 10;
  int isKeyword(const char *word);
  int isOperator(char ch);
 void lexicalAnalysis(const char* filename);
 
  int main()
  {
          const char* filename = "input.txt";
          printf("Lexical Analysis of %s: \n\n",filename);
          lexicalAnalysis(filename);
          return 0;
  }
 
  int isKeyword(const char*word)
  {
          for(int i=0;i<keywordcount;i++)
          {
                  if(strcmp(word,keywords[i]) == 0)
                  {
                          return 1;
                  }
          }
          return 0;
 }
int isOperator(char ch)
  {
         char operators[] = "(){}+-*/=><";
          for(int i=0;i<strlen(operators);i++)
          {
                  if(ch == operators[i])
                  {
                          return 1;
                  }
          }
          return 0;
  }
   void lexicalAnalysis(const char * filename)
  {
          FILE* file = fopen(filename,"r");
          if(file == NULL)
         {
                  printf("Error: Could not open file %s\n",filename);
                  exit(1);
         }
          char ch;
          char buffer[50];
          int i=0;
          while((ch=fgetc(file))!=EOF)
          {
                  if(isOperator(ch))
                          printf("Operator: %c\n",ch);
                  else if(isalnum(ch))
                          buffer[i++]=ch;
                  else if((ch==' ' || ch=='\n' ||ch=='\t') && i>0)
                  {
                          buffer[i] ='\0';
                          i=0;
                          if(isKeyword(buffer))
                          {
                                  printf("Keyword: %s\n",buffer);
                          }
                          else
                          {
                                  printf("Identifier: %s\n",buffer);
                          }
                 }
         }
  fclose(file);
 }
