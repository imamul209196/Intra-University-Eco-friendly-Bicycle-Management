#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <string.h>
#include <time.h>
#include <windows.h>

struct cycle
{
    char cycleName[10];
    struct cycle *next;
};
typedef struct cycle cycle;
cycle *top;
int size;

struct type
{
    char fname[30];
    char lname[30];
    int id;
    char phone[12];
    char day[4], month[4], date[3], time[10], year[5];
    char d[4], m[4], da[3], t[10], y[5];
    char cycle_No[7];
};
typedef struct type type;

struct node
{
    char name[20];
    int id;
    char phone[12];
    char check_out_date_and_time[30];
    char check_in_Date_and_time[30];
    char cycle_No[10];
    struct node *next;
};

typedef struct node node;

node *head;
node *head_of_the_History;

void cycleStore();
void createlist();
void display();
void insert_begining();
void insert_end();
void delete();
void insert_position();
int count();
int search_node();
void edit();
void delete();
void History();
void addedToFile();
void readToFile();
char *liveTime();

int cnt();
int isEmpty();
int isFull();
void push();
cycle *pop();

void ccolor(int clr)
{

    HANDLE hConsole;
    hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
    SetConsoleTextAttribute(hConsole, clr);
}

void mainFunc()
{
    int n;
    system("cls");
    time_t t;
    time(&t);
    printf("\n\t\t\t\t\t   Current Date/Time = %s\n\n", ctime(&t));
    printf("\t\t\t\t\t ___________________________________________________\t\t\n");
    printf("\t\t\t\t\t|                                                   |\t\t\n");
    printf("\t\t\t\t\t|                  Service Available                |\t\t\n");
    printf("\t\t\t\t\t|                  7 days in a week                 |\t\t\n");
    printf("\t\t\t\t\t|                       24/7                        |\t\t\n");
    printf("\t\t\t\t\t|___________________________________________________|\t\t\n\n\n");
}

int main()
{
    ccolor(2);
    printf("\n\n\n\n\n\n\n\n");
    printf("\t\t\t\t ____________________________________________\t\t\n");
    printf("\t\t\t\t|                                            |\t\t\n");
    printf("\t\t\t\t|                WELCOME TO                  |\t\t\n");
    printf("\t\t\t\t|        Intra University Ecofriendly        |\t\t\n");
    printf("\t\t\t\t|              Bycycle Service               |\t\t\n");
    printf("\t\t\t\t|____________________________________________|\t\t\n");

    printf("\t\t\t\t ____________________________________________\t\t\n");
    printf("\t\t\t\t|                                            |\t\t\n");
    printf("\t\t\t\t|      Daffodil International University     |\t\t\n");
    printf("\t\t\t\t|       Birulia - 1216, Dhaka, Bangladesh.   |\t\t\n");
    printf("\t\t\t\t|____________________________________________|\t\t\n");

    printf("\n\n\t\t\t\t");

    for (int j = 0; j < 40; j++)
    {
        Sleep(60);
        if (j < 1)
            printf("L");
        if (j == 5)
            printf("O");
        if (j == 11)
            printf("A");
        if (j == 17)
            printf("D");
        if (j == 24)
            printf("I");
        if (j == 30)
            printf("N");
        if (j == 39)
            printf("G");
        else
        {
            printf("_");
        }
    }
    Sleep(1600);
    mainFunc();
    printf("Press any key to go to Main Menu\n");
    getch();
    cycleStore();

    int a;
    while (1)
    {
        printf("\nMain Manu :\n\n");
        printf("1. Create List\t\t\t2. Display List\n\n");
        printf("3. Check out\t\t\t4. Search & Edit & Check in\n\n");
        printf("5. Today's History\t\t6. All History\n\n");
        printf("7. Available Cycle\t\t8. Exit\n\n");
        printf("Enter your Choice :");
        scanf("%d", &a);
        printf("\n");
        switch (a)
        {
        case 1:
            createlist();
            break;
        case 2:
            display();
            break;
        case 3:
            insert_begining();
            break;
        case 4:
            search_node();
            break;
        case 5:
            History();
            break;
        case 6:
            readToFile();
            break;
        case 7:
            printf("There are %d cycle available!", cnt());
            printf("\n\nPress any key to go to Main Manu\n");
            getch();
            break;
        case 8:
            if (count(head) == 0)
            {
                return 0;
            }
            else
            {
                int z;
                printf("%d Users check in is pending!\n", count(head));
                printf("Do you still want to exit?\n\n1. Yes\t2.No\n\nEnter your choice :");
                scanf("%d", &z);
                if (z == 1)
                {
                    return 0;
                }
                printf("\nPress any key to go to Main Menu");
                getch();
            }
            break;
        default:
            printf("Invalid Choice\n");
            printf("Press any key to go to Main Menu");
            getch();
            break;
        }
    }
}

void cycleStore()
{
    size = 50;
    top = (cycle *)malloc(sizeof(cycle));
    strcpy(top->cycleName, "G1C1");
    cycle *temp;
    temp = top;
    for (int i = 1, j = 2, k = 2; j <= 50; j++, k++)
    {
        cycle *newnode;
        newnode = (cycle *)malloc(sizeof(cycle));
        sprintf(newnode->cycleName, "G%dC%d", i, k);
        if (j == 10)
        {
            i++;
        }
        if (j == 20)
        {
            i++;
        }
        if (j == 30)
        {
            i++;
        }
        if (j == 40)
        {
            i++;
        }
        if (j == 50)
        {
            i++;
        }
        if (j % 10 == 0)
        {
            k = 0;
        }
        temp->next = newnode;
        temp = temp->next;
    }
}

void createlist()
{
    int n;
    printf("How many User you wnat to add in this list : ");
    scanf("%d", &n);
    node *newnode, *temp;
    head = (node *)malloc(sizeof(node));
    printf("Name : ");
    fflush(stdin);
    gets((head)->name);
    printf("ID :");
    scanf("%d", &head->id);
    printf("Enter Phone Number :");
    fflush(stdin);
    gets(head->phone);
    /*printf("Check out date :");
    fflush(stdin);
    gets(head->check_out_date);
    printf("Check out time :");
    fflush(stdin);
    gets(head->check_out_time);*/
    char *s = liveTime();
    s[strlen(s) - 1] = '\0';
    strcpy(head->check_out_date_and_time, s);
    printf("Cycle No :");
    fflush(stdin);
    gets(head->cycle_No);
    head->next = NULL;
    temp = head;
    for (int i = 1; i < n; i++)
    {
        newnode = (node *)malloc(sizeof(node));
        printf("Name :");
        fflush(stdin);
        gets((newnode)->name);
        printf("ID :");
        scanf("%d", &newnode->id);
        printf("Enter Phone Number :");
        fflush(stdin);
        gets(newnode->phone);
        /*printf("Check out date :");
        fflush(stdin);
        gets((newnode)->check_out_date);
        printf("Check out time :");
        fflush(stdin);
        gets((newnode)->check_out_time);*/
        char *s = liveTime();
        s[strlen(s) - 1] = '\0';
        strcpy(newnode->check_out_date_and_time, s);
        printf("Cycle No :");
        fflush(stdin);
        gets(newnode->cycle_No);
        newnode->next = NULL;
        temp->next = newnode;
        temp = temp->next;
    }
    printf("\nUser Information taken successfully!\n\nPress any key to go to Main Memu\n");
    getch();
}

void display()
{
    node *temp;
    temp = head;
    printf("    Full-Name\t\tID\tPhone Number\tCheckout_Date_and_Time\t\tCycle_No\n");
    int i = 1;
    while (temp != NULL)
    {
        printf("%d. ", i);
        printf("%s      ", temp->name);
        printf("\t%d\t", temp->id);
        printf("%s\t", temp->phone);
        // printf("%s\t", temp->check_out_date);
        // printf("%s\t\t", temp->check_out_time);
        printf("%s\t", temp->check_out_date_and_time);
        printf("%s\n", temp->cycle_No);
        temp = temp->next;
        i++;
    }
    printf("\nPress any key to go to Main Menu\n");
    getch();
}

void insert_begining()
{
    node *newnode;
    newnode = (node *)malloc(sizeof(node));
    printf("Name :");
    fflush(stdin);
    gets((newnode)->name);
    printf("ID :");
    scanf("%d", &newnode->id);
    printf("Enter Phone Number :");
    fflush(stdin);
    gets(newnode->phone);
    /*printf("Check out date :");
    fflush(stdin);
    gets((newnode)->check_out_date);
    printf("Check out time :");
    fflush(stdin);
    gets((newnode)->check_out_time);*/
    char *s = liveTime();
    s[strlen(s) - 1] = '\0';
    strcpy(newnode->check_out_date_and_time, s);
    // printf("Cycle No :");
    //  fflush(stdin);
    //  gets(newnode->cycle_No);
    strcpy(newnode->cycle_No, pop());
    newnode->next = head;
    head = newnode;
    printf("\nNew User information added successfully!\n");
    printf("\nPress any key to go to Main Menu\n");
    getch();
}

int count(node *temp)
{
    int c = 0;
    while (temp != NULL)
    {
        temp = temp->next;
        c++;
    }
    return c;
}

int search_node()
{
    int id;
    printf("Enter ID :");
    scanf("%d", &id);
    node *temp;
    temp = head;
    while (temp != NULL && temp->id != id)
    {
        temp = temp->next;
    }
    if (temp == NULL)
    {
        printf("User not found not found\n");
        printf("\nPress any key to go to Main Menu\n");
        getch();
        return 0;
    }
    else
    {
        printf("    Full-Name\t\tID\tPhone Number\tCheckout_Date_and_Time\t\tCycle_No\n");
        printf("1. ");
        printf("%s      ", temp->name);
        printf("\t%d\t", temp->id);
        printf("%s\t", temp->phone);
        // printf("%s\t", temp->check_out_date);
        // printf("%s\t\t", temp->check_out_time);
        printf("%s\t", temp->check_out_date_and_time);
        printf("%s\n\n", temp->cycle_No);
    }
    while (1)
    {
        int a;
        printf("1. Edit\t\t2. Check in\n\n3. Main menu\n");
        printf("Enter your choice :");
        scanf("%d", &a);
        switch (a)
        {
        case 1:
            edit(temp);
            return 0;
        case 2:
            delete (temp);
            return 0;
        case 3:
            return 0;
        default:
            printf("Invalid choice\n");
            break;
        }
    }
}

void edit(node *temp)
{
    printf("Do you want to edit Name\n\n");
    printf("1. Yes\t2. No\n");
    int b;
    scanf("%d", &b);
    if (b == 1)
    {
        printf("Write new name :");
        fflush(stdin);
        gets(temp->name);
    }
    printf("Do you want to edit ID\n\n");
    printf("1. Yes\t2. No\n");
    int c;
    scanf("%d", &c);
    if (c == 1)
    {
        printf("Write new ID :");
        scanf("%d", &temp->id);
    }
    printf("Done\n");
    printf("\nPress any key to go to Main Menu\n");
    getch();
}

void delete(node *p)
{

    node *temp, *q;
    temp = head;
    if (p == head)
    {
        head = temp->next;
        if (count(head_of_the_History) == 0)
        {
            // printf("%d\n", count(head_of_the_History));
            // head_of_the_History = (node *)malloc(sizeof(node));
            head_of_the_History = temp;
            char *s = liveTime();
            s[strlen(s) - 1] = '\0';
            strcpy(head_of_the_History->check_in_Date_and_time, s);
            head_of_the_History->next = NULL;
            addedToFile(head_of_the_History);
        }
        else
        {
            node *tem;
            node *newnode;
            // newnode = temp;
            // newnode = (node *)malloc(sizeof(node));
            newnode = temp;
            // newnode = p;
            char *s = liveTime();
            s[strlen(s) - 1] = '\0';
            strcpy(newnode->check_in_Date_and_time, s);
            addedToFile(newnode);
            tem = head_of_the_History;
            while (tem->next != NULL)
            {
                tem = tem->next;
            }
            tem->next = newnode;
            newnode->next = NULL;
        }
        push(temp);
        // free(temp);
        // temp = NULL;
        printf("Check in successfully done!\n");
        printf("\nPress any key to go to Main Menu\n");
        getch();
    }
    else
    {
        q = temp->next;
        while (q->id != p->id)
        {
            temp = q;
            q = temp->next;
        }
        temp->next = q->next;
        if (count(head_of_the_History) == 0)
        {
            // printf("%d\n", count(head_of_the_History));
            // head_of_the_History = (node *)malloc(sizeof(node));
            head_of_the_History = q;
            char *s = liveTime();
            s[strlen(s) - 1] = '\0';
            strcpy(head_of_the_History->check_in_Date_and_time, s);
            head_of_the_History->next = NULL;
            addedToFile(head_of_the_History);
        }
        else
        {
            node *tem;
            node *newnode;
            // newnode = (node *)malloc(sizeof(node));
            newnode = q;
            char *s = liveTime();
            s[strlen(s) - 1] = '\0';
            strcpy(newnode->check_in_Date_and_time, s);
            tem = head_of_the_History;
            while (tem->next != NULL)
            {
                tem = tem->next;
            }
            tem->next = newnode;
            newnode->next = NULL;
            addedToFile(newnode);
        }
        push(q);
        // free(q);
        // q = NULL;
        printf("Check in successfully done!\n");
        printf("\nPress any key to go to Main Menu\n");
        getch();
    }
}

void History()
{
    node *temp;
    temp = head_of_the_History;
    printf("    Full-Name\t\tID\tPhone Number\tCheckout_Date_and_Time\t\tCheckin_Date_and_Time\t\tCycle_No\n");
    int i = 1;
    while (temp != NULL)
    {
        printf("%d. ", i);
        printf("%s      ", temp->name);
        printf("\t%d\t", temp->id);
        printf("%s\t", temp->phone);
        // printf("%s\t", temp->check_out_date);
        // printf("%s\t\t", temp->check_out_time);
        printf("%s\t", temp->check_out_date_and_time);
        printf("%s\t", temp->check_in_Date_and_time);
        printf("%s\n", temp->cycle_No);
        temp = temp->next;
        i++;
    }
    printf("\nPress any key to go to Main Menu\n");
    getch();
}

void addedToFile(node *temp)
{
    FILE *file = fopen("list.txt", "a");
    if (file == NULL)
    {
        printf("File not opened\n");
        exit(1);
    }
    // fprintf(file, "%d. ", z);
    fprintf(file, "%s      ", temp->name);
    fprintf(file, "\t%d\t", temp->id);
    fprintf(file, "%s\t", temp->phone);
    // fprintf(file, "%s\t", temp->check_out_date);
    // fprintf(file, "%s\t\t", temp->check_out_time);
    fprintf(file, "%s\t", temp->check_out_date_and_time);
    fprintf(file, "%s\t\t", temp->check_in_Date_and_time);
    fprintf(file, "%s\n", temp->cycle_No);
    temp = temp->next;
    fclose(file);
}

void readToFile()
{
    FILE *file = fopen("list.txt", "r");
    if (file == NULL)
    {
        printf("File empty!");
        printf("\nPress any key to go to Main Menu\n");
        getch();
        exit(2);
    }
    type temp;
    printf("    Full-Name\t\tID\tPhone Number\tCheckout_Date_and_Time\t\tCheck_in_Date_and_Time\t\tCycle_No\n");
    int i = 1;
    while (fscanf(file, "%s %s", &temp.fname, &temp.lname) >= 0)
    {
        fscanf(file, "\t%d\t", &temp.id);
        fscanf(file, "%s\t", &temp.phone);
        // fscanf(file, "%s\t", &temp.check_out_date);
        // fscanf(file, "%s\t\t", &temp.check_out_time);
        fscanf(file, "%s %s %s %s %s\t", &temp.day, &temp.month, &temp.date, &temp.time, &temp.year);
        fscanf(file, "%s %s %s %s %s\t", &temp.d, &temp.m, &temp.da, &temp.t, &temp.y);
        fscanf(file, "%s\n", &temp.cycle_No);
        printf("%d. ", i);
        printf("%s %s      ", temp.fname, temp.lname);
        printf("\t%d\t", temp.id);
        printf("%s\t", temp.phone);
        // printf("%s\t", temp.check_out_date);
        // printf("%s\t\t", temp.check_out_time);
        printf("%s %s %s %s %s\t", temp.day, temp.month, temp.date, temp.time, temp.year);
        printf("%s %s %s %s %s\t", temp.d, temp.m, temp.da, temp.t, temp.y);
        printf("%s\n", temp.cycle_No);
        i++;
    }
    fclose(file);
    printf("\nPress any key to go to Main Menu\n");
    getch();
}

char *liveTime()
{
    time_t t;
    time(&t);
    return ctime(&t);
}

int cnt()
{
    cycle *temp;
    int c = 0;
    temp = top;
    while (temp != NULL)
    {
        c++;
        temp = temp->next;
    }
    return c;
}

int isEmpty()
{
    if (top == NULL)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}

int isFull()
{
    if (cnt() == size)
    {
        return 1;
    }
    return 0;
}

void push(node *temp)
{
    if (isFull())
    {
        printf("Stack Overflow\n");
    }
    else
    {
        cycle *newnode;
        newnode = (cycle *)malloc(sizeof(cycle));
        strcpy(newnode->cycleName, temp->cycle_No);
        newnode->next = NULL;
        if (isEmpty())
        {
            top = (cycle *)malloc(sizeof(cycle));
            top = newnode;
            top->next = NULL;
        }
        else
        {
            newnode->next = top;
            top = newnode;
        }
    }
}

cycle *pop()
{
    if (isEmpty())
    {
        printf("Stack Underflow\n");
    }
    else
    {
        cycle *temp;
        temp = top;
        top = top->next;
        return temp;
    }
}
