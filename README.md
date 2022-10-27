# Matlab example Hopfield networks

    T = [1 -1; -1 1; 1 1; -1 -1]';
    plot(T(1,:),T(2,:),'*r')

    axis([-1.1 1.1 -1.1 1.1])
    title('Точки рівноваги мережі Хопфілда')
    xlabel('a(1)'), ylabel('a(2)')


    net = newhop(T);
    W = net.LW{1,1}
    b = net.b{1,1}


    Ai = T;
    [Y,Pf,Af] = sim(net,4,[],Ai)

    plot(T(1,:), T(2,:),'*r', 0,0,'rh'), hold on, axis([-1.1 1.1 -1.1 1.1]) 
    xlabel('a(1)'), ylabel('a(2)')

    new = newhop(T); 

    [Y,Pf,Af] = sim(net,4,[],T); 
    for i = 1:20
        a = {rands(2,1)};

        [Y, Pf, Af] = sim(net,{1,20},{},a); record = [cell2mat(a) cell2mat(Y)]; start = cell2mat(a);

        plot(start(1,1),start(2,1),'kx',record(1,:),record(2,:)) 
    end

    color = 'rgbmy';
    for i=1:25
       a = {rands(2,1)};
       [y,Pf,Af] = net({20},{},a);
       record=[cell2mat(a) cell2mat(y)];
       start=cell2mat(a);
       plot(start(1,1),start(2,1),'kx',record(1,:),record(2,:),color(rem(i,5)+1))
    end


    [alphabet, targets] = prprob;
    i = 1;
    ti = alphabet(:, i);
    ti
    letter{i} = reshape(ti, [5,7])'
    letter{i}
    plotchar(reshape(letter{i}', 1, 35)');
    net = newhop(letter{i});
    [Y,Pf,Af] = sim(net,5,[], letter{i});


    noisyA = alphabet(:,1) + randn(35,1) *0.4;
    reshape(noisyA, 5, 7)'

    plotchar(noisyA);

    [Y,Pf,Af] = sim(net,5,[],reshape(noisyA, 5, 7)');


    plotchar(reshape(Y', 1, 35)');




