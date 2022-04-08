#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<conio.h>
//Structure to hold the content of each record
struct Data{
int cid;	// Customer ID
char *source;	// Restaurant
char *dest;	// Destination point
char *time;	// Time order was placed
int did;	// Delivery agent assigned to this order

};
int delcount[5]={0,0,0,0,0};	// To store number of deliveries for each agent
struct Data src[10];
int reccount=0;
void DelPerson(void);
void printData(void);
void printEarnings(void);
void printTotalEarnings(void);
void SetDel(void);

int timediff(char*,char*);	// To check if two orders are within 15 min
void TohandleBooking(){
FILE *fp;
char input[30][100],*token,*token1;
int j=0,cid[30];
fp=fopen("input.txt","r");
if(fp==NULL)
{
printf("File empty\n");
exit(0);
}
// Read file one record at a time, split into fields and store in memory
while(!feof(fp))
{
fgets(input[j],100,fp);
token=strtok(input[j],",");
src[j].cid=token[0]-48;
token1=strtok(NULL,"\n");
token=strtok(token1,",");
src[j].source=token;
token1=strtok(NULL,"\n");
token=strtok(token1,",");
src[j].dest=token;
token1=strtok(NULL,"\n");
src[j].time=token1;
src[j].did=-1;
j++;
reccount++;	// to keep count of records in file
}
}
int main(){
printf("\nFOOD DELIVERY SYSTEM\n");
TohandleBooking();
DelPerson();
printData();
SetDel();
printTotalEarnings();
getch();
clrscr();
return 0;
}
// Temp function, not used
void printData()
{
	printf ("ID\tSource\tDestination\tTime\n");
  for (int i = 0; i < 5; i++)
  {
	printf ("%d\t%s\t%s\t%s\n", src[i].cid,src[i].source,src[i].dest,src[i].time);
  }
}
// To print empty records first time
void DelPerson()
{
char *de[10]= {"DE1","DE2","DE3","DE4","DE5"};
int da[5]={0,0,0,0,0};
int i,j;

printf ("Available executives: \n");
for(i=0;i<5;i++)
{
	printf("%s  %d  ",de[i],da[i]);
}
printf ("\n");
}
// Convert 24 hr format to min and find the diff. Return 1 if within limits
int timediff( char x[], char y[])
{
char tmp1[30],tmp2[30];
char *token2,*token1;
int hr1,min1,hr2,min2,total1,total2;

strcpy (tmp1,x);
strcpy(tmp2,y);
token1=strtok(x,":");
hr1=atoi(token1);
token1=strtok(NULL,'\0');
min1=atoi(token1);
total1=hr1*60+min1;
token2=strtok(y,":");
hr2=atoi(token2);
token2=strtok(NULL,'\0');
min2=atoi(token2);
total2=hr2*60+min2;
strcpy (x,tmp1);
strcpy (y,tmp2);
if(abs(total1-total2)<=15)
{
return 1;
}
else
{
return 0;
}
}
// To set the delivery agent for each order and to count orders per agent
void SetDel()
{
int currentId=-1,i=0,j=0;
for(i=0;i<reccount;i++)
{
	if(src[i].did<0)
	{
	       src[i].did=++currentId;
	       delcount[currentId]++;
	       for(j=i+1;j<reccount;j++)
	       {
			if(
			(strcmp(src[j].dest,src[i].dest)==0)
			&&
			(timediff(src[j].time,src[i].time)==1)
			)
		       {
			       src[j].did=currentId;
			       delcount[currentId]++;
		       }
	       }
	}
       printEarnings();
}
}
// To print the report as provided
void printEarnings()
{
	int i = 0;
printf ("EXECUTIVES\t\tEARNINGS\n");
for(i=0;i<5;i++)
{
printf ("DE%d\t\t\t",i+1);
printf("%d",(delcount[i] > 0) ? (50+((delcount[i]-1) * 5)):0);
printf("\n");
}
}
// To print allowance for only agents who delivered
void printTotalEarnings()
{
	int i = 0;
	printf ("EXECUTIVES\t\tALLOWANCE\t\tEARNINGS\t\tTOTAL\n");
	for(i=0;i<5;i++)
	{
		if (delcount[i] > 0)
		{
			printf ("DE%d\t\t\t10\t\t%d\t\t%d",i+1,(50+((delcount[i]-1) * 5)),(60+((delcount[i]-1) * 5)));
			printf("\n");
		}
	}
}


