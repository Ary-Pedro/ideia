#afazer
Estudar pelo: [profissionaloracle.com.br](http://profissionaloracle.com.br/)  
  
Sites [draw.io](http://draw.io/), [Db Designer](https://erd.dbdesigner.net/dashboard)
  
2 oracle tem OTN (grupo de usuário da oracle) revistas e máteriais  
  
3 oracle live (disponibiliza dados e tutoria de trigger) 
(site para uso, coddar)  
  
4 tirar certificação oracle coursera oracle <sup>feito</sup>

# oracle apex
```Sql
select * from dept  
  
select * from emp  
  
-- 1 selecionar Nome cargo salário dos empregados que ganham abaixo da média sálarial  
select ename,job,sal from emp where sal <(select avg(sal)from emp);  
  
  
-- 2 selecionar Nome do empregado seu salário comissão e vencimento  
select ename nome, sal salário, comm comissão,  sal+nvl(comm,0) vencimento from emp  
-- erro na soma de sal + comm  retorna null se uma for null ignorando o valor da outra;  
  
  
-- 3 selecionar nome do empregado e nome do seu departamento  
select ename, dname from emp e,dept d where e.deptno=d.deptno  
  
  
-- 4 selecionar  nome do departameto a média sálarial e total de salario  
select d.dname, avg(e.sal), sum (e.sal)  
from emp e, dept d  
where e.deptno=d.deptno  
group by d.dname  
-- erro incrementar o group by para fazer a manupulação de avg e sum  
  
  
-- 5 selecionar  nome do departamento total de salarios, o maior salario e departamento que possua mais que 3 empregado  
select d.dname, sum(e.sal), max(e.sal)  
from emp e, dept d  
where e.deptno=d.deptno  
group by d.dname  
having count(*)>3  
  
--  join  
select DEPT.DNAME as DNAME,  
    EMP.ENAME as ENAME,  
    EMP.JOB as JOB,  
    EMP.SAL as SAL  
 from EMP EMP,  
    DEPT DEPT  
 where DEPT.DEPTNO=EMP.DEPTNO
```

Veja detalhes em [[Resumo das aulas]]
