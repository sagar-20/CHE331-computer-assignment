# CHE331-computer-assignment

% Define rate expression parameters
% 
k1 = input('Enter the value of K1 = ');
K2 = input('Enter the value of K2 = ');
Ca0 = input('Starting point for Ca = ');
Ca1 = input('Ending point for Ca = ');
P = input('The point for derivative = ');
x1= input('The starting x cordinate = ');
x2= input('The ending x cordinate = ');
% k1 = 1;
% K2 = 3;
% Ca0 = 0;
% Ca1 = 10;
% P = 0.5;
% x1 = 1;
% x2 = 6;


% Define Ca range
Ca = Ca0:0.01:Ca1;

% Calculate reaction rate (-rA) as a function of Ca
rate = k1*Ca./(1+K2*Ca.^2);

% (a) Calculate derivative at a point Ca=0.5
d_rate = diff(rate)./diff(Ca);
derivative = d_rate(find(Ca>=P,1));

% (b) Calculate area under the curve using trapezoidal rule
area = trapz(Ca,rate);

% (c) Find maximum functional value and corresponding Ca value
[max_rate, max_index] = max(rate);
[min_rate,i] =  min(rate);
min_Ca = Ca(i);
max_Ca = Ca(max_index);
% min_Ca = Ca(min_index1);

% (d) Drawing a straight line between two points (Ca1,rate1) and (Ca2,rate2)
Ca1 = x1;
rate1 = k1*Ca1./(1+K2*Ca1.^2);
Ca2 = x2;
rate2 = k1*Ca2./(1+K2*Ca2.^2);
m = (rate2-rate1)/(Ca2-Ca1);
c = rate1 - m*Ca1;
line_Ca = x1:0.01:x2;
line_rate = m*line_Ca + c;
plot(Ca,rate,'b','LineWidth',2);
grid on
hold on
plot(line_Ca,line_rate,'r','LineWidth',2);
xlabel('Ca');
ylabel('Rate');
title('Rate vs Concentration for -r_A = k1Ca/(1+k2Ca^2)')



% (e) Find point where the tangent is the same as the given slope from
% previous question
mini = 1e12;
min_index =x1;
prev = x1;
for c1 = x1:0.01:x2
%     disp(c);
      if c1 == x1
          continue;
      end
     curr_tan = (k1*c1/(1+K2*c1^2)-k1*prev/(1+K2*prev^2))/0.01;
     prev = c1;
     if(abs(curr_tan-m)<mini)
         mini = abs(curr_tan-m);
         min_index = c1;
     end
end
hold on
plot(min_index,k1*min_index/(1+K2*min_index^2),'xr','LineWidth',4);
legend('rate vs concentration','line between two points','point with the tangent
same as the slope of the line ')
hold off

%Printing the output
fprintf('\nThe derivaive at %f point = %f\n',P,derivative);
fprintf('Area under the curve = %f\n',area);
fprintf('Maxima %f occurs at %f\n',max_rate,max_Ca);
fprintf('Minima %f occurs at %f\n',min_rate,min_Ca);
fprintf('The line between the points is y = %fx+%f\n',m,c);
fprintf('Point where the tangent is the same as the given slope (%f) is =
%f\n',m,min_index);
