function iteration_methodfnc(Xin,Yin,Tol)

X0=Xin;
Y0=Yin;
itr=0;
error=1;
while error>Tol
[Fx,Fx0,Fy0]=f(X0,Y0);
[Gx,Gx0,Gy0]=g(X0,Y0);
    itr=itr+1;
    fprintf('iteration=%d\n',itr);
D=[Fx0 Gx0 0 0;Fy0 Gy0 0 0;0 0 Fx0 Gx0;0 0 Fy0 Gy0];
b=[-1;0;0;-1];

if det(D)==0
    disp('change the initial approximation')
else
    A=inv(D)*b;
end
x1= X0+A(1)*Fx+A(2)*Gx;
y1= Y0+A(3)*Fx+A(4)*Gx;

    valueini=[X0;Y0];
    valuefin=[x1;y1];
    error=norm(valueini-valuefin,inf);
    
    X0=x1;
    Y0=y1;
end
fprintf('Maximum iteration=%d\n',itr)
fprintf('Required solution is x=%f and y=%f\n',x1,y1)
