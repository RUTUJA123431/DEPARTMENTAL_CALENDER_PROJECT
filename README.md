#include<stdio.h>
#include<string.h>

#define MAX_EVENTS 100
#define MAX_MONTHS 12

typedef struct{
    char name[50];
    char date[20];
}Event;

typedef struct{
    char month[20];
    Event events[MAX_EVENTS];
    int eventCount;
}Month;

void addEvent(Month *month,const char *eventName,const char *eventDate){
    if (month->eventCount <MAX_EVENTS)
{
    strcpy(month->events[month->eventCount].name,eventName);
    strcpy(month->events[month->eventCount].date,eventDate);
    month->eventCount++;
}else{
    printf("Max event limit reached for %s\n",month->month);
}
}
void displayCalender(Month months[]){
    for(int i=0;i<MAX_MONTHS;i++){
        printf("Month: %s\n",months[i].month);
    for(int j=0;j<months[i].eventCount;j++){
        printf("Event: %s on %s\n",months[i].events[j].name,months[i].events[j].date);
    }
    printf("\n");
    }
}

int get_first_weekDay(int year) {
	int day;
	day = (((year - 1) * 365) + ((year - 1) / 4) - ((year - 1) / 100) + ((year) / 400)) % 7;
	return day;
}

int main(){
    Month months[MAX_MONTHS]=
{
    {"january",{},0},
    {"february",{},0},
    {"march",{},0},
    {"april",{},0},
    {"may",{},0},
    {"june",{},0},
    {"july",{},0},
    {"august",{},0},
    {"september",{},0},
    {"october",{},0},
    {"november",{},0},
    {"december",{},0},
};
//adding events
addEvent(&months[0],"New Year Celebration","01-01");
addEvent(&months[1],"basant panchmi","14-02");
addEvent(&months[2],"holi","08-03");
addEvent(&months[3],"GUdhi padwa","09-04");
addEvent(&months[4],"Maharashtra din","01-05");
addEvent(&months[5],"bakri eid","17-06");
addEvent(&months[6],"Guru paurnima","21-07");
addEvent(&months[7],"INDEPENDENCE DAY","15-08");
addEvent(&months[8],"ganesh chaturthi","07-09");
addEvent(&months[9],"Dashera","12-10");
addEvent(&months[10],"diwali","01-11");
addEvent(&months[11],"merry christmas","25-12");

//semester exams
addEvent(&months[4],"MID SEMESTER EXAMS","15-05");
addEvent(&months[7],"unit test","15-08");

addEvent(&months[11],"END SEMESTER EXAMS","9-12");

//DISPLAYING THE CALENDER
displayCalender(months);

	int year, day = 0, dayInMonth, weekDay = 0, startingDay, month;
	printf("Enter Year: ");
	scanf("%d", &year);

	char *months1[] = {"January", "February", "March", "April", "May", "June",
	                  "July", "August", "September", "October", "November", "December"
	                 };
	int monthDays[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

	if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
		monthDays[1] = 29;
	}

	startingDay = get_first_weekDay(year);

	for (month = 0; month < 12; month++) {
		dayInMonth = monthDays[month];
		printf("\n\n--------------------%s---------------------", months1[month]);
		printf("\n Sun  Mon  Tue  Wed  Thu  Fri  Sat\n");

		for (weekDay = 0; weekDay < startingDay; weekDay++) {
			printf("     ");
		}

		for (day = 1; day <= dayInMonth; day++) {
			printf("%5d", day);
			if (++weekDay > 6) {
				printf("\n");
				weekDay = 0;
			}
		}

		startingDay = weekDay;
	}

	return 0;
}
