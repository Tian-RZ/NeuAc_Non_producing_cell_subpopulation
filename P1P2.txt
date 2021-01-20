function Model_Subpopulations_NeuAc_Yiled
% NeuAc biosynthesis model in the presence and absence of non-producing subpopulations

close all
clear
clc
% Input of cell growth data
x=[2.5 5 7.5 10 13 16 20 23.5 27 32.5 38.5 48 54 60];
y=[0.00 0.27 0.74 1.36 3.17 4.88 6.93 7.78 8.02 8.63 9.05 9.06 9.39 9.54];
% Fit the growth curve
xi=2.5:0.01:60;
yi=interp1(x,y,xi,'spline');

% NeuAc titer in the presence of non-producing subpopulations
% The proportion of non-producing subpopulations is calculated according to experimental results:
% I_Nonproducing(%) = 1.0729 * yi + 17.833
i=1;
y_Nonproducing=zeros(1,576);
y_producing=zeros(1,576);
yield_before=zeros(1,576);
for time=2.51:0.01:60
    i=i+1;
    y_Nonproducing(i)=yi(i)*(1.0729*time + 17.833)/100;
    y_producing(i)=yi(i)-y_Nonproducing(i);
    yield=1*0.01*y_producing(i);
    yield_before(i)=yield_before(i-1)+yield;
end
b_eNY=y_Nonproducing;
b_eY=y_producing;
b_yield=yield_before;

% NeuAc titer in the absence of non-producing subpopulations
i=1;
for time=2.51:0.01:60
    i=i+1;
    y_producing(i)=yi(i);
    yield=1*0.01*y_producing(i);
    yield_before(i)=yield_before(i-1)+yield;
end
a_eY=y_producing;
a_yield=yield_before;


figure(1)
subplot(1,2,1)
y2=0;
shadedplot(xi,b_eY,y2,'g')
hold on
[AX,H1,H2]=plotyy(xi,yi,xi,b_yield,@plot);
set(H1,'color','r','LineWidth',2);
set(H2,'color','b','LineWidth',2);
hold on
set(get(AX(1),'ylabel'),'string', 'Biomass','fontsize',16,'color','k');
set(get(AX(2),'ylabel'),'string', 'NeuAc (a.u.)','fontsize',16,'color','k');
xlabel('Time (h)','fontsize',16);
hold on
plot(x,y,'o');
set(gcf,'color','white')
set(gca,'linewidth',2)
set(AX(1), 'YColor', 'k','yTick',0:2:10,'fontsize',16)
set(AX(2), 'YColor', 'k','yLim',[0,400],'yTick',0:100:400,'fontsize',16)
grid off;

subplot(1,2,2)
plot(x,y,'o')
hold on
[AX,H1,H2]=plotyy(xi,yi,xi,a_yield,@plot);
set(H1,'color','r','LineWidth',2);
set(H2,'color','b','LineWidth',2);
hold on
set(get(AX(1),'ylabel'),'string', 'Biomass','fontsize',16,'color','k');
set(get(AX(2),'ylabel'),'string', 'NeuAc (a.u.)','fontsize',16,'color','k');
xlabel('Time (h)','fontsize',16);
hold on
y2=0;
shadedplot(xi,a_eY,y2,'g')
set(gcf,'color','white')
set(gca,'linewidth',2)
set(AX(1), 'YColor', 'k','yTick',0:2:10,'fontsize',16)
set(AX(2), 'YColor', 'k','yLim',[0,400],'yTick',0:100:400,'fontsize',16)
grid off;
end
