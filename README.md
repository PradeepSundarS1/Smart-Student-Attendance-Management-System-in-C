# Smart-Student-Attendance-Management-System-in-C

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct student 
{
    char name[100];
    int stuid;
    char dept[100];
    int year;
};
struct attendance
{
    int stuid;
    char date[100];
    char status[10];
};
void addstudent();
void viewallstudent();
void markattendance();
void viewreport();
int main()
{
    int choice;
    while (1)
    {
        printf("\n===== SMART ATTENDANCE SYSTEM =====\n");
        printf("1) ADD STUDENT\n");
        printf("2) VIEW ALL THE STUDENT\n");
        printf("3) MARK ATTENDANCE\n");
        printf("4) VIEW REPORT OF THE STUDENT\n");
        printf("0) EXIT\n");
        printf("ENTER A VALID NUMBER\n");
        scanf("%d",&choice);
        switch (choice)
        {
            case 1:
                addstudent();
                break;
           case 2 : 
                viewallstudent();
                break; 
           case 3 : 
                markattendance();
                break;
           case 4 :
                viewreport();
                break; 
           case 0 : 
                printf("===== PROGRAM EXIT =====\n");
                exit(0);
                break;
           default : 
                printf("ENTER VALID NUMBER\n");
                break;
        }
    }
}
void addstudent()
{
    struct student s;
    FILE *fp;
    fp=fopen("student.dat","ab");
    if (fp==NULL)
        printf("NO FILE FOUND\n");
    printf("ENTER THE STUDENT NAME : ");
    scanf(" %[^\n]", s.name);
    printf("ENTER STUDENT ID : ");
    scanf("%d",&s.stuid);
    printf("ENTER STUDENT DEPARTMENT : ");
    scanf(" %[^\n]", s.dept);
    printf("ENTER STUDENT YEAR : ");
    scanf("%d",&s.year);
    fwrite(&s,sizeof(s),1,fp);
    fclose(fp);
    printf("STUDENT REGISTERED SUCCESSFULLY!!!\n");
}
void viewallstudent()
{
    struct student s;
    FILE *fp;
    fp=fopen("student.dat","rb");
    if (fp==NULL)
        printf("NO FILE FOUND\n");
    while(fread(&s,sizeof(s),1,fp))
    {
        printf("NAME : %s\n",s.name);
        printf("ID : %d\n",s.stuid);
        printf("DEPARTMENT : %s\n",s.dept);
        printf("YEAR : %d\n\n",s.year);
    }
    fclose(fp);
}
int count()
{
    struct student s;
    FILE *fp;
    int count=0;
    fp=fopen("student.dat","rb");
    if (fp==NULL)
        printf("NO FILE FOUND\n");
    while (fread(&s,sizeof(s),1,fp))
    {
        count++;
    }
    fclose(fp);
    return count;
}
void markattendance()
{
    struct attendance a;
    FILE *fp;
    fp=fopen("attendance.dat","ab");
    if (fp==NULL)
        printf("NO FILE FOUND\n");
    int totalstu;
    totalstu=count();
    if (totalstu == 0)
    {
        printf("NO STUDENTS FOUND. ADD STUDENTS FIRST.\n");
        fclose(fp);
        return;
    }
     if (fp==NULL)
        printf("NO FILE FOUND\n");
    printf("ENTER DATE : ");
    scanf(" %[^\n]", a.date);
    for (int i=0;i<totalstu;i++)
    {
        printf("ENTER STUDENT ID : ");
        scanf("%d",&a.stuid);
        printf("ENTER PRESENT(P) OR ABSENT(A) : ");
        scanf("%s",a.status);
        fwrite(&a,sizeof(a),1,fp);
    }
    fclose(fp);
}
void viewreport()
{
    struct attendance a;
    FILE *fp;
    int total=0,pre=0,id;
    float percentage;
    printf("ENTER STUDENT ID : ");
    scanf("%d",&id);
    fp=fopen("attendance.dat","rb");
    if (fp==NULL)
        printf("NO FILE FOUND\n");
    while(fread(&a,sizeof(a),1,fp))
    {
        if (a.stuid==id)
        {
            total++;
            if (strcmp(a.status, "P") == 0)
                pre++;
        }
    }
    percentage = (pre * 100.0) / total;
    printf("TOTAL DAYS = %d\n",total);
    printf("PRESENT DAYS = %d\n",pre);
    printf("ATTENDANCE PERCENTAGE = %.2f\n",percentage);

}
```
## OUTPUT
<img width="1865" height="1029" alt="1" src="https://github.com/user-attachments/assets/61683806-d988-4a60-b752-8418b7d3b76f" />
<img width="1855" height="1008" alt="2" src="https://github.com/user-attachments/assets/a7d59ac6-5500-4ff9-a511-30887a51481a" />
<img width="1862" height="305" alt="3" src="https://github.com/user-attachments/assets/411cb659-d547-4e7b-b3fd-bb4e38352b18" />

