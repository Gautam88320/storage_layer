# storage_layer
Mongo_sql
For MySQL and MongoDB	
1	 Display all the information of the EMP table?
         select * from emp;
	 db.emp.find({ });
2	 Display unique Jobs from EMP table?
         select distinct(job ) from emp;
 	 db.emp.find({},{
         "distinct(job)": 1 });
3	 List the emps in the asc order of their Salaries?
         select * from emp order by sal asc;
 	 db.emporder by sal asc.find({}).sort({"sal": 1});
4	 List the details of the emps in asc order of the Dptnos and desc of Jobs?
         select * from emp order by deptno asc, job desc;
	  db.emporder by deptno asc, job desc.find({}).sort({"deptno": -1});
5	 Display all the unique job groups in the descending order?
	 select distinct (job) from emp order by job desc;
	  db.emporder by job desc.find({},{  "distinct(job)": 1}).sort({"job": -1});
6	 Display all the details of all ‘Mgrs’
	 select * from emp where job='manager';
	 db.emp.find({"job" : 'manager'});
7	 List the emps who joined before 1981
	 select * from emp where hiredate <('1981-1-1'); 
	 db.emp.find({"hiredate ":{ "$lt" : ('1981-1-1' }});
8	 List the Empno, Ename, Sal, Daily sal of all emps in the asc order of Annsal
	 select empno,ename,sal, sal/30 as dailysal, sal*12 as annsal from emp order by annsal asc;
	 db.emporder by annsal asc.find({ },{
   "empno": 1,
   "ename": 1,
   "sal": 1,
   "sal/30asdailysal": 1,
   "sal*12asannsal": 1
}
).sort({
  "annsal": 1
});
         select empno,ename,sal, sal/30 dailysal, sal*12 annsal from emp order by annsal asc;        ----(as not mand..)
9	 Display the Empno, Ename, job, Hiredate, Exp of all Mgrs
	 select empno,ename,job,hiredate, timestampdiff(year,hiredate,curdate()) exp from emp where in(select mgr from emp);
	db.emp.find({
 "": {"$in": [select mgr from emp}
},{
   "empno": 1,
   "ename": 1,
   "job": 1,
   "hiredate": 1,
   "timestampdiff(year": 1,
   "hiredate": 1,
   "curdate())exp": 1
}
);
10	 List the Empno, Ename, Sal, Exp of all emps working for Mgr 7369
	 select empno,ename,sal,exp from emp where mgr = 7369; 	 
          db.emp.find({
 "mgr " :  7369
},{
   "empno": 1,
   "ename": 1,
   "sal": 1,
   "exp": 1
}
);
11	 Display all the details of the emps whose Comm  Is more than their Sal
         select * from emp where comm > sal; 
          db.emp.find({
 "$where": "this.comm  > this. sal"
});
13	 List the emps along with their Exp and Daily Sal is more than Rs 100
	  select * from emp where (sal/30) >100;
           db.emp.find({
 "sal/30) ":{ "$gt" : 100 }
});
14	 List the emps who are either ‘CLERK’ or ‘ANALYST’ in the Desc order
	  select * from emp where job = ‘CLERK’ or job = ‘ANALYST’ order by job desc;
          db.emp.find({

   "$or": [{
    "$where": "this.job  == this. ‘CLERK’ "
 },{ "$where": "this.job  == this. ‘ANALYST’ "
   }]
}).sort({
 "job": -1
});

15	 List the emps who joined on 1-MAY-81,3-DEC-81,17-DEC-81,19-JAN-80 in asc order of seniority
 	 select * from emp where hiredate in (’01-may-81’,’03-dec-81’,’17-dec81’,’19-jan-80’) order by hiredate asc; 
   	  db.emp.find({
 "hiredate": {"$in":  [’01-may-81’,’03-dec-81’,’17-dec81’,’19-jan-80’] }
}).sort({
 "hiredate": 1
});
16	 List the emp who are working for the Deptno 10 or20
 	 select * from emp where deptno = 10 or deptno = 20 ;
	 db.emp.find({

   "$or": [{
    "deptno " :  10 
 },{ "deptno " :  20 
   }]
});
17	 List the emps who are joined in the year 81
 	 select * from emp where hiredate between ’01-jan-81’ and ’31-dec-81’; 
	 db.emp.find({

   "$and": [{
   
 },{ 
   }]
});

19	 List the emps Who Annual sal ranging from 22000 and 45000
 	  select * from emp where 12*sal between 22000 and 45000;
20	 List the Enames those are having five characters in their Names
 	  select ename from emp where length (ename) = 5;
	  db.emp.find({
 "length (ename) " :  5
},{
   "ename": 1
}
);
21	 List the Enames those are starting with ‘S’ and with five characters
	  select ename from emp where ename like ‘S%’ and length (ename) = 5;
 		db.emp.find({

   "$and": [{
   "$where": "this.ename  == this. ‘S%’ "
 },{ " length (ename) " :  5
   }]
},{
   "ename": 1
}
);
22	 List the emps those are having four chars and third character must be ‘r’
 	  select * from emp where length(ename) = 4 and ename like ‘__R%’;
	  db.emp.find({

   "$and": [{
   "length(ename) " :  4 
 },{ "$where": "this. ename  == this. ‘__R%’"
   }]
});
23	 List the Five character names starting with ‘S’ and ending with ‘H’
 	  select * from emp where length(ename) = 5 and ename like ‘S%H’; 
 	db.emp.find({

   "$and": [{
   "length(ename) " :  5 
 },{ "$where": "this. ename  == this. ‘S%H’"
   }]
});
24	 List the emps who joined in January
 	 select * from emp where to_char (hiredate,’mon’) = ‘jan’; 
          db.emp.find({
 "$where": "this.to_char (hiredate,’mon’)  == this. ‘jan’"
});	 
27	 List the emps whose names having a character set ‘ll’ together
	 select * from emp where ename like ‘%LL%’; 
          db.emp.find({
 "$where": "this.ename  == this. ‘%LL%’"
});
29	 List the emps who does not belong to Deptno 20
	  select * from emp where deptno != 20;
           db.emp.find({
 "deptno " : { "$ne":  20}
});
30	 List all the emps except ‘PRESIDENT’ & ‘MGR” in asc order of Salaries
	 Select * from emp where job not in (‘PRESIDENT’,’MANAGER’) order by sal asc;
	 db.emp.find({
 "jobnot ": {"$in":  [‘PRESIDENT’,’MANAGER’] }
}).sort({
 "sal": 1
});
31	 List the emps whose Empno not starting with digit78
	  select * from emp where empno not like ‘78%’; 
	   db.emp.find({
 "empno not " :  ‘78%’
});
33	 List the emps who are working under ‘MGR’
	 select e.ename || ‘ works for ‘ || m.ename from emp e ,emp m where e.mgr =m.empno ;
 	  db.empe ,emp m .find({
 "$where": "this.e.mgr  == this.m.empno "
},{
   "e.ename||‘worksfor‘||m.ename": 1
}
);
34	 List the emps who joined in any year but not belongs to the month of March
	 select * from emp where to_char (hiredate,’MON’) not in (‘MAR’);
	 db.emp.find({
 "to_char(hiredate,’MON’) not ": {"$in":  [‘MAR’}
});
35	 List all the Clerks of Deptno 20
	 select * from emp where job =‘CLERK’ and deptno = 20; 
	 db.emp.find({

   "$and": [{
   "$where": "this.job  == this.‘CLERK’ "
 },{ " deptno " :  20
   }]
});
36	 List the emps of Deptno 30 or 10 joined in the year 1981
	 select * from emp where to_char (hiredate,’YYYY’) in (‘1981’) and (deptno = 30 or deptno =10 ) ;
     		db.emp.find({

   "$and": [{
   "to_char(hiredate,’YYYY’) ": {"$in":  [‘1981’] } 
    },{
   "$or": [{
    "deptno " :  30 
 },{ "deptno " : 10 ) 
   }]
   }]
});
37	 Display the details of SMITH
	 select *from emp where ename='smith';
          db.emp.find({
 "ename" : 'smith'
});
38	 Display the location of SMITH
         select loc from emp e , dept d where e.ename = ‘SMITH’ and e.deptno =d.deptno ; 

       db.empe , dept d .find({

   "$and": [{
   "$where": "this.e.ename  == this. ‘SMITH’ "
 },{ "$where": "this. e.deptno  == this.d.deptno "
   }]
},{
   "loc": 1
}
);
    
