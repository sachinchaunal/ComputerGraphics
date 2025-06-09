#include <graphics.h>
void hut()
{
	int gd= DETECT, gm;
	initgraph(&gd,&gm,"");
//HUT
	rectangle(150,250,350,400);
	rectangle(220,320,280,400);
	line(150,250,250,150);
	line(250,150,350,250);
	getch();
}


void drawPie()
{
	int gd= DETECT, gm;
	initgraph(&gd,&gm,"");
//PIE
	setfillstyle(SOLID_FILL,RED);
	pieslice(200,200,0,45,100);
	setfillstyle(SOLID_FILL,BLUE);
	pieslice(200,200,45,90,100);
	setfillstyle(SOLID_FILL,GREEN);
	pieslice(200,200,90,360,100);
	getch();
}


void barchart()
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	//BAR
	setcolor(WHITE);
	bar(100,200,150,400);
	bar(200,250,250,400);
	bar(300,300,350,400);
	line(50,50,50,410);
	line(50,410,400,410);
	getch();
}


void increasingCircle()
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	
	for(int i=20;i<200;i+=20)
	{
		circle(300,300,i+20);
		delay(300);
	}
	getch();
}


void movingCar()
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	
	for(int i=0;i<400;i+=10)
	{
		cleardevice();
		rectangle(50+i,100,200+i,200);
		circle(70+i,200,10);
		circle(180+i,200,10);
		delay(100);
	}
	
	getch();
}


void rainbow()
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	
	for(int i=0;i<7;i++)
	{
		setcolor(i+1);
		arc(300,300,0,180,100+(i*10));
		delay(100);
	}
	getch();
	closegraph();
}


void smiley()
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	
	circle(300,300,100);
	circle(250,250,10);
	circle(350,250,10);
	arc(300,300,210,330,20);
	
	getch();
}


void trafficLight()
{
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "");
    rectangle(200, 100, 300, 400);
    setcolor(WHITE); // outline color for floodfill border
    setfillstyle(SOLID_FILL, RED);
    circle(250, 150, 40);
    floodfill(250, 150, WHITE);  // fill inside circle
    delay(500);
    setfillstyle(SOLID_FILL, YELLOW);
    circle(250, 250, 40);
    floodfill(250, 250, WHITE);
    delay(500);
    setfillstyle(SOLID_FILL, GREEN);
    circle(250, 350, 40);
    floodfill(250, 350, WHITE);

    getch();
    closegraph();
}


void DDA(int x1,int y1,int x2,int y2)
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	
	int dx=x2-x1,dy=y2-y1,steps;
	float xinc,yinc,x=x1,y=y1;
	steps=abs(dx) > abs(dy) ? abs(dx) : abs(dy);
	
	xinc=dx/(float)steps;
	yinc=dy/(float)steps;
	
	for(int i=0;i<=steps;i++)
	{
		putpixel(x,y,WHITE);
		x+=xinc;
		y+=yinc;
		delay(10);
	}
	getch();
}

void bresenham(int x1,int y1, int x2, int y2)
{
//	when slope is btw 0 and 1
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	
	int dx=x2-x1,dy=y2-y1,p=2*dy-dx;
	int x=x1,y=y1;
	
	while(x1<=x2)
	{
		putpixel(x,y,WHITE);
		x++;
		
		if(p<0)
		{
			p=p+2*dy;	
		}
		else
		{
			p+=2*(dy-dx);
			y++;	
		}
		delay(10);
	}
	
	getch();
}

void midpoint(int xc,int yc,int r)
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	
	int x=0,y=r,p=1-r;
	while(x<=y)
	{
		putpixel(xc+x,yc+y,WHITE);
		putpixel(xc-x,yc+y,WHITE);
		putpixel(xc+x,yc-y,WHITE);
		putpixel(xc-x,yc-y,WHITE);
		putpixel(xc+y,yc+x,WHITE);
		putpixel(xc-y,yc+x,WHITE);
		putpixel(xc+y,yc-x,WHITE);
		putpixel(xc-y,yc-x,WHITE);
		x++;
		if(p<0)
		{
			p+=2*x+1;
		}
		else
		{
			y--;
			p+=2*(x-y)+1;	
		}
	}
	getch();	
}


void text()
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	outtextxy(200,200,"hello" );
	getch();
}



void boundary(int x,int y, int f, int b)
{
	if(getpixel(x,y)!=b && getpixel(x,y)!=f)
	{
		putpixel(x,y,f);
		
		boundary(x+1,y,f,b);
		boundary(x,y+1,f,b);
		boundary(x-1,y,f,b);
		boundary(x,y-1,f,b);
		
		boundary(x-1,y-1,f,b);
		boundary(x-1,y+1,f,b);
		boundary(x+1,y-1,f,b);
		boundary(x+1,y+1,f,b);
	}
	
}

void flood(int x,int y,int n,int old)
{
	
	if(getpixel(x,y)==old)
	{
		putpixel(x,y,n);
		
		flood(x+1,y,n,old);
		flood(x,y+1,n,old);
		flood(x-1,y,n,old);
		flood(x,y-1,n,old);
		
		flood(x+1,y-1,n,old);
		flood(x-1,y-1,n,old);
		flood(x+1,y+1,n,old);
		flood(x-1,y+1,n,old);
	}

}
int main()
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,"");
	
	
//	setcolor(WHITE);  // border color
//    rectangle(100, 100, 300, 200);
    // Call boundary fill from inside the rectangle
//    boundary(150, 150, RED, WHITE);  // fill inside with RED
    
    setcolor(WHITE);
    rectangle(100, 100, 300, 200);

    // Fill inside the rectangle using flood fill
    int fill_start_x = 50, fill_start_y = 50;
    int old_color = getpixel(fill_start_x, fill_start_y);
    flood(fill_start_x, fill_start_y, RED, old_color);
    
	getch();
}



