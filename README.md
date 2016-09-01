#include <iostream>
#include <string>
#include <cstdlib>

using namespace std;

struct StudentRecord
{
       char name[20];
       char roll[20];
	float m1, m2, m3;
       float gpa;
       float avg;
       struct StudentRecord *next;   //venky remember check addition of word struct
} *head;

class stud
{
 public: 

	StudentRecord *newStudentRecord(char*, char*,float,float,float,float);
	
     char sname[20], sroll[20];  
     float sm1, sm2, sm3, sgpa;

void getdata();
void display();
float stud::avgfind(float,float,float);
float gpafind(float,float,float);
void searchtopper();
void displaytopper();

stud()
{    head=NULL; }

};

int main() 
{
   cout << "Student Record Program" << endl << endl;
	
	int ch;
	stud ss; 
	head=NULL;
	while(1)
	{
	cout << "1. Enter a student record " << endl;
	cout << "2. List all student records " << endl;
	cout << "3. Display topper details " << endl;
	cout << "4. Exit program " << endl;
	cout << endl <<"What would you like to do?" << endl;
	cin>>ch;
	switch(ch)
	 {
	  case 1:   cout<<"\n You chose 1 \n";
			ss.getdata();
			break;
	  case 2:   cout<<"\n You chose 2 \n";
			ss.display();
			break;
	  case 3:   cout<<"\n You chose 3 \n";
			ss.displaytopper();
			break;
	  case 4:   cout<<"\n EXIT";
			exit(1);  break;
	 }
	}
}

StudentRecord *stud::newStudentRecord(char sname[],char sroll[],float sm1, float sm2, float sm3, float sgpa)
{
 struct StudentRecord *temp, *s;
 temp=new (struct StudentRecord);
  if (temp==NULL)
  {   cout<<"\n MEMORY NOT ALLOCATED\n";
	return 0;
 }
else
{
  strcpy(temp->name,sname);
  strcpy(temp->roll,sroll);
  temp->m1=sm1;
  temp->m2=sm2;
  temp->m3=sm3;
  temp->avg=savg;
  temp->gpa=sgpa;
  temp->next=NULL;
  return temp;
 }
}

void stud::getdata()
{
cout << "student name: ";
cin>> sname;
cout << "student roll: ";
cin >> sroll;
cout << "Marks 1: ";
cin >> sm1;
cout << "Marks 2: ";
cin >> sm2;
cout << "Marks 3: ";
cin >> sm3;
savg=avgfind(sm1,sm2,sm3);
sgpa= gpafind(sm1,sm2,sm3);

struct StudentRecord *temp, *p;
temp=newStudentRecord(sname,sroll,sm1,sm2,sm3,sgpa);
if (head==NULL)
 {
  head=temp;
  head->next=NULL;
}
else 
{
 p=head;
head=temp;
head->next=p;
}
cout<<"\n info stored \n";
}


	/*                 
                     if(!head)
                       head = newStudentRecord;
                     else
                     {
                         StudentRecord_ptr = head;
        
                         while(StudentRecord_ptr -> next)
                            StudentRecord_ptr = StudentRecord_ptr -> next;
           
                            StudentRecord_ptr -> next = newStudentRecord;
                      } */

void stud::display()
{
cout << endl << "Listing all student records: \n";
	                           
		struct StudentRecord *Display_ptr;
                     Display_ptr = head;
           
                     while(Display_ptr != NULL)
                     {
                        cout <<" Student name: "<< Display_ptr -> name << endl;
                        cout <<" Student roll: "<< Display_ptr -> roll << endl;
                        cout <<" Marks 1: "<< Display_ptr -> m1 << endl;
			cout <<" Marks 2: "<< Display_ptr -> m2 << endl;
			cout <<" Marks 3: "<< Display_ptr -> m3 << endl;
			cout <<" Student final AVERAGE is :"<< Display_ptr -> avg << endl;
                        cout <<" Student final GPA is :"<< Display_ptr -> gpa << endl;
            
                        Display_ptr = Display_ptr -> next;
                        cout << endl;
                      }cout<<"\n";
}

float stud::gpafind(float v1,float v2,float v3)
{
  float tot, avg, cgpa;
   tot=v1+v2+v3;
   avg=tot/3;
   cgpa=avg/10;
   

return cgpa;
}
float stud::avgfind(float v1,float v2,float v3)
{
  float tot, avg;
   tot=v1+v2+v3;
   avg=tot/3;
   return avg;
}

void stud::searchtopper()
{
    int value, pos = 0;
    bool flag = false;
    if (head == NULL)
    {
        cout<<"List is empty"<<endl;
        return;
    }

    cout<<"Enter the value to be searched: ";
    cin>>value;

    struct StudentRecord *s;
    s = head;
    while (s != NULL)
    {
        pos++;
       if (s->gpa == value)
        {

           flag = true;
            cout<<"Element "<<value<<" is found at position "<<pos<<endl;
		cout<<"\n name of topper is: "<<s->name<<" and his roll no.is "<<s->roll;        
}

        s = s->next;
    }
    if (!flag)
        cout<<"Element "<<value<<" not found in the list"<<endl;  

}

 void stud::displaytopper()

{
   float max;
   char tname[20];
   char troll[20];
   bool flag = false;
    if (head == NULL)
    {
        cout<<"List is empty"<<endl;
        return;
    }
     struct StudentRecord *s;
    s = head;

    max=s->gpa;
     while (s!=NULL)
     {
       if (s->gpa>=max)
       {
         flag=true;
            strcpy(tname,s->name);
            strcpy(troll,s->roll);
      }
        s=s->next;
     }
       cout<<"\n The topper is : "<< tname<<"\n";
}
