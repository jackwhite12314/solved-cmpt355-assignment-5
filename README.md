Download Link: https://assignmentchef.com/product/solved-cmpt355-assignment-5
<br>
<h1>Part 1: Indexes /40</h1>

<strong> </strong>

The last thing we’ll be doing with our employee database is adding a few indexes. After adding each index, run the associated query/queries and record the performance (planning time and execution time). Also look at the explain plan of the queries. <em>You’ll probably need to rewrite the queries slightly to fit your database (if there are different columns or tables).  </em>




Index 1: Add an index to the employee_histories table first_name and last_name fields.

Index 2: Add an index to the employee_jobs table employee_id and job_id fields. Index 3: Add an index to the employees table birthdate field.




For each index, answer the following questions:

<ol>

 <li>Fill out the tables below describing how adding the index affected the planning and execution timings.</li>

 <li>Did adding the index change the explain plans? What changed?</li>

 <li>Was this what you expected to happen for the timing and the execution plans? What is a possible reason for this change (or lack of change)?</li>

</ol>




<h1>Index 1</h1>

<table width="437">

 <tbody>

  <tr>

   <td width="161"><strong>Execution Time </strong></td>

   <td width="140">Without index</td>

   <td width="136">With index</td>

  </tr>

  <tr>

   <td width="161">Query 1</td>

   <td width="140"> </td>

   <td width="136"> </td>

  </tr>

  <tr>

   <td width="161">Query 2</td>

   <td width="140"> </td>

   <td width="136"> </td>

  </tr>

 </tbody>

</table>




<h1>Index 2</h1>

<table width="437">

 <tbody>

  <tr>

   <td width="161"><strong>Execution Time </strong></td>

   <td width="140">Without index</td>

   <td width="136">With index</td>

  </tr>

  <tr>

   <td width="161">Query 3</td>

   <td width="140"> </td>

   <td width="136"> </td>

  </tr>

  <tr>

   <td width="161"> <strong>Index 3 </strong></td>

   <td width="140"> </td>

   <td width="136"> </td>

  </tr>

  <tr>

   <td width="161"><strong>Execution Time </strong></td>

   <td width="140">Without index</td>

   <td width="136">With index</td>

  </tr>

  <tr>

   <td width="161">Query 4</td>

   <td width="140"> </td>

   <td width="136"> </td>

  </tr>

 </tbody>

</table>










<h1>Part 2: Normalization /40</h1>

<strong> </strong>

Let’s pretend that the company whose employees we’ve been managing so far is an engineering firm. The company manages multiple projects at a time, and assigns its employees to tasks on the different projects. Only one employee can be assigned to a project task. Below is some un-normalized data used to manage projects in a company. After analyzing this sample data, structure it in 1<sup>st</sup> normal, 2<sup>nd</sup> normal, and 3<sup>rd</sup> normal form one step at a time, showing the results of each step. So you should have 3 diagram – one for your data in 1<sup>st</sup> normal, one for 2<sup>nd</sup> normal, and one for 3<sup>rd</sup> normal.







<table width="639">

 <tbody>

  <tr>

   <td width="61">TeamMemberId</td>

   <td width="68">TeamMemberFirstName</td>

   <td width="61">TeamMemberLastName</td>

   <td width="53">Project Code</td>

   <td width="96">Project Name</td>

   <td width="66">Project Status</td>

   <td width="72">Project Manager</td>

   <td width="59">TaskNumber</td>

   <td width="102">Task Status</td>

  </tr>

  <tr>

   <td width="61">1</td>

   <td width="68">John</td>

   <td width="61">Smith</td>

   <td width="53">DDL</td>

   <td width="96">Darren &amp; Darren Ltd</td>

   <td width="66">Active</td>

   <td width="72">Garth Butler</td>

   <td width="59">10132133134</td>

   <td width="102">ResolvedIn ProgressNot StartedIn Progress</td>

  </tr>

  <tr>

   <td width="61">2</td>

   <td width="68">Dave</td>

   <td width="61">Richter</td>

   <td width="53">DDL  KMI</td>

   <td width="96">Darren &amp;Darren Ltd Kristen MotorsInc.</td>

   <td width="66">Active  Active</td>

   <td width="72">GarthButler Jim David</td>

   <td width="59">100110 1013</td>

   <td width="102">In ProgressNot Started Not StartedResolved</td>

  </tr>

  <tr>

   <td width="61">3</td>

   <td width="68">Janie</td>

   <td width="61">Klotter</td>

   <td width="53">KMI</td>

   <td width="96">Kristen MotorsInc.</td>

   <td width="66">Active</td>

   <td width="72">Jim David</td>

   <td width="59">1215</td>

   <td width="102">In ProgressResolvedResolved</td>

  </tr>

 </tbody>

</table>







<strong> </strong>

<h1>Part 3: Concurrency /20</h1>

<strong> </strong>

<ol>

 <li>Scenario – Transaction A and B are being run concurrently in separate sessions.</li>

</ol>




Below is the initial state of the Accounts table before any transaction is run

<table width="243">

 <tbody>

  <tr>

   <td width="78">Account Number</td>

   <td width="68">Account Nickname</td>

   <td width="97">Account Balance</td>

  </tr>

  <tr>

   <td width="78">1</td>

   <td width="68">Chequing</td>

   <td width="97">450</td>

  </tr>

  <tr>

   <td width="78">2</td>

   <td width="68">Chequing</td>

   <td width="97">200</td>

  </tr>

 </tbody>

</table>































<table width="624">

 <tbody>

  <tr>

   <td width="312">Transaction A</td>

   <td width="312">Transaction B</td>

  </tr>

  <tr>

   <td width="312">SET TRANSACTION ISOLATION LEVEL READUNCOMMITTED;BEGIN SELECTa.account_number,a.account_nickname,a.account_balanceFROM accounts;  UPDATE accountsSET account_balance = 0WHERE account_number = 2;                 END;COMMIT;</td>

   <td width="312">SET TRANSACTION ISOLATION LEVEL READUNCOMMITTED;BEGIN             SELECTa.account_number,a.account_nickname,a.account_balanceFROM accounts; UPDATE accountsSET account_balance = account_balance – 100WHERE account_number = 1; UPDATE accountsSET account_balance = account_balance + 100WHERE account_number = 2;  END;COMMIT;</td>

  </tr>

 </tbody>

</table>










<ol>

 <li>What would the Accounts table look like after these transactions are finished?</li>

</ol>




<table width="243">

 <tbody>

  <tr>

   <td width="78">Account Number</td>

   <td width="68">Account Nickname</td>

   <td width="97">Account Balance</td>

  </tr>

  <tr>

   <td width="78"> </td>

   <td width="68"> </td>

   <td width="97"> </td>

  </tr>

  <tr>

   <td width="78"> </td>

   <td width="68"> </td>

   <td width="97"> </td>

  </tr>

 </tbody>

</table>




<ol>

 <li>What type(s) of data inconsistency is caused in this case (lost update, dirty read, nonrepeatable read, or phantom read)?</li>

</ol>




<ol start="2">

 <li>Transaction C and D are being run concurrently in separate sessions Below is the initial state of the Accounts table before any transaction is run:</li>

</ol>

<table width="243">

 <tbody>

  <tr>

   <td width="78">Account Number</td>

   <td width="68">Account Nickname</td>

   <td width="97">Account Balance</td>

  </tr>

  <tr>

   <td width="78">1</td>

   <td width="68">Chequing</td>

   <td width="97">450</td>

  </tr>

  <tr>

   <td width="78">2</td>

   <td width="68">Chequing</td>

   <td width="97">200</td>

  </tr>

 </tbody>

</table>










<table width="624">

 <tbody>

  <tr>

   <td width="312">Transaction C</td>

   <td width="312">Transaction D</td>

  </tr>

  <tr>

   <td width="312">SET TRANSACTION ISOLATION LEVEL READCOMMITTED;BEGIN SELECTa.account_number,a.account_nickname,a.account_balanceFROM accounts;           SELECTa.account_number,a.account_nickname,a.account_balanceFROM accounts;  END;COMMIT;</td>

   <td width="312">SET TRANSACTION ISOLATION LEVEL READCOMMITTED;BEGIN         INSERT INTO accounts (account_number, account_nickname, account_balance)VALUES(3, ‘Savings’, 50); UPDATE accountsSET account_balance = 300WHERE account_number = 1; END;COMMIT;      </td>

  </tr>

 </tbody>

</table>







<ol>

 <li>What type(s) of data inconsistency is caused in this case (lost update, dirty read, nonrepeatable read, or phantom read)?</li>

</ol>




<ol start="3">

 <li>Transaction E and F are being run concurrently in separate sessions</li>

</ol>

Below is the initial state of the Accounts table before any transaction is run:

<table width="243">

 <tbody>

  <tr>

   <td width="78">Account Number</td>

   <td width="68">Account Nickname</td>

   <td width="97">Account Balance</td>

  </tr>

  <tr>

   <td width="78">1</td>

   <td width="68">Chequing</td>

   <td width="97">450</td>

  </tr>

  <tr>

   <td width="78">2</td>

   <td width="68">Chequing</td>

   <td width="97">200</td>

  </tr>

 </tbody>

</table>










<table width="624">

 <tbody>

  <tr>

   <td width="312">Transaction E</td>

   <td width="312">Transaction F</td>

  </tr>

  <tr>

   <td width="312">SET TRANSACTION ISOLATION LEVEL UNCOMMITTEDREAD;BEGIN SELECTa.account_number,a.account_nickname,a.account_balanceFROM accounts;  UPDATE accountsSET account_balance = 300WHERE account_number = 1;        SELECTa.account_number,a.account_nickname,a.account_balanceFROM accounts; END;ROLLBACK ;</td>

   <td width="312">SET TRANSACTION ISOLATION LEVEL UNCOMMITTEDREAD; BEGIN            SELECTa.account_number,a.account_nickname,a.account_balanceFROM accounts;           INSERT INTO accounts (account_number, account_nickname, account_balance)VALUES(3, ‘Savings’, 50); END;COMMIT;</td>

  </tr>

 </tbody>

</table>







<ol>

 <li>What type(s) of data inconsistency is caused in this case (lost update, dirty read, nonrepeatable read, or phantom read)?</li>

</ol>


