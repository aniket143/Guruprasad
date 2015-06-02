<?php 
 include('connection.php');
 header("Access-Control-Allow-Origin:*");
$current_date = date("Y-m-d H:i:s");
date_default_timezone_set("Asia/Calcutta");
$qualify=500;
$customerQualfiyAmount=1000;
$memberId=$_POST['member1'];

$bill_num=$_POST['billno'];

$amount=$_POST['amount'];

$totalamount=$_POST['amount'];
$payment=$_POST['payment'];	
$net=$_POST['net'];	
$sms=$_POST['sms'];	
$s_code=$_POST['t1'];

$commission=$_POST['com'];	
		
$tot=($totalamount*$commission)/100;
$tot1=($tot*30)/100;
$tot2=($tot*70)/100;


 include('connection.php');
   

$query="INSERT INTO BILL_DETAIL values('','$memberId','$bill_num','$amount','$totalamount','$tot1','N','','$current_date','tie_up')";

             // mysql_query("INSERT INTO BILL_DETAIL VALUES ('','$client_cd','$Bill_no','$mrp','$Final_total','$customer_price','N','$username','$current_date','shop')" )or die('INSERT INTO BILL_DETAIL Query Failed: ' .mysql_error());
              mysql_query("INSERT INTO BILL_DETAIL_MSG VALUES ('','$memberId','$bill_num','$amount','$totalamount','$tot1','N','$s_code','$current_date','MOBILE_SHOP','$sms')" )or die('INSERT INTO BILL_DETAIL_MSG Query Failed: ' .mysql_error());
              mysql_query("INSERT INTO BILL_DETAIL VALUES ('','$memberId','$bill_num','$amount','$totalamount','$tot1','N','$s_code','$current_date','MOBILE_SHOP')" )or die('INSERT INTO BILL_DETAIL Query Failed: ' .mysql_error());
             mysql_query("INSERT INTO confirm_order VALUES ('','$memberId','$Pt_code','$Pname','$Final_qty','$amount','$totalamount','$tot1','$current_date','$current_date','N','$bill_num','$s_code')" )or die('INSERT INTO final_bill Query Failed: ' .mysql_error());
             $sql1="select sum(totalamount) as total,sum(totalpoint) as tpoint from BILL_DETAIL where memberId='$memberId' and qualify='N'";
            // echo $sql1.'<br>';
             $resultSet1=mysql_query($sql1) or die("InsertQuery Failed:".mysql_error());
             $row=mysql_fetch_assoc($resultSet1);
             if ($row['total']>=$qualify)
             {
    	$sql4="select  * from BILL_DETAIL where memberId='$memberId' and qualify='N' order by sr_no LIMIT 0,1";
    //	echo $sql4.'<br>';
		$resultSet4=mysql_query($sql4) or die("Query Failed4:".mysql_error());
		$row4=mysql_fetch_assoc($resultSet4);
		
		$sql51="select  * from BILL_DETAIL where memberId='$memberId' and qualify='N' order by sr_no desc LIMIT 0,1";
		    	//echo $sql51.'<br>';
		$resultSet51=mysql_query($sql51) or die("Query Failed5:".mysql_error());
		$row51=mysql_fetch_assoc($resultSet51);
		$rtr="select  max(`sr_no`) as srnoo from BILL_DETAIL";
		$resultrtr=mysql_query($rtr) or die("Query Failed5:".mysql_error());
		while($rowrtr=mysql_fetch_assoc($resultrtr))
		{
			 $srnoo=$rowrtr['srnoo'];
			}
		
		$crd=0;
		$tot=0;
		$dbt=0;
		$less=0;
		$schg=0;
		$gross=0;
		$tds=0;
		$net=0;

	    mysql_query("Insert into  member_point_table values('','$memberId','".$row['total']."','$tot1','N','0','','$current_date','$current_date','".$srnoo."','".$srnoo."','','','','','$crd','$tot','$dbt','$less','$schg','$gross','$tds','$net','n')") or die("Member Achieve Point Query Failed:".mysql_error());
		mysql_query("update confirm_order set qualify='Y' where memberId='$memberId' and qualify='N'") or die("Confirm Order Query Failed:".mysql_error());
		mysql_query("update BILL_DETAIL set qualify='Y' where memberId='$memberId' and qualify='N'") or die("Confirm Order Query Failed:".mysql_error());
         
       $rand=mt_rand();
	   mysql_query("Insert Into fra_bill_det values('','$user','$memberId','".$row['total']."','','$current_date','$rand','".$bill_num."')") or die("Query Failed6:".mysql_error());
	  $point1=$row["tpoint"];
	  
	  $sql5="select  * from member_point_table where pointachieve='N' order by id LIMIT 0,1";
	  $resultSet5=mysql_query($sql5) or die("Query Failed5:".mysql_error());
	  $row5=mysql_fetch_assoc($resultSet5);
      if(($row5["totalpoint"]+$point1)>=$row5["point"])
		{
			 
}   
}		



/*******************1*********************8*/
$sql55="select  * from member_point_table where pointachieve='N'";
//echo $sql55;
	  $resultSet55=mysql_query($sql55) or die("Query Failed5:".mysql_error());
	  $row55=mysql_fetch_assoc($resultSet55);
      //if(($row5["totalpoint"]+$point1)>=$row5["point"])
      if(mysql_num_rows($resultSet55)>0)
		{
			
			$ppp="select sum(`totalpoint`) as tpoint from `BILL_DETAIL`";
			$ppp1=mysql_query($ppp);
			while($ppp2=mysql_fetch_assoc($ppp1))
			 {
			 	$gsumm=$ppp2['tpoint'];
			 	}
			 	
    $kkr="SELECT sum(`totalpoint`) as summer FROM member_point_table WHERE `totalpoint`<=1000";
    $kkr1=mysql_query($kkr);
    while($kkr2=mysql_fetch_assoc($kkr1))
     {
     	$summer=$kkr2['summer'];
     	}
     				

     				
     	$remainpoint=$gsumm-$summer;
     	$nr=$remainpoint / 1000;
     	$nr1=explode('.', $nr);
     	$noe=$nr1[0];
     	$k=0;
     	$bbb="SELECT * FROM member_point_table WHERE pointachieve='N'";
     	$bbb1=mysql_query($bbb);
     	while($bbb2=mysql_fetch_assoc($bbb1))
     	 {
     	 	$gid=$bbb2['id'];
     	 	$memid=$bbb2['memid'];
     	 	$cdd=$bbb2['crd'];
     	 	
     	 	if($k<$noe)
     	 	{    	 		
     	 		$crds=0;
     	 		
		 $zzz="SELECT * FROM member_point_table WHERE `pointachieve`='Y' AND `pt_status`='n' AND id<$gid AND `memid` IN (SELECT `memberId` FROM `member_registration` WHERE `sponsorId`='$memid')";
     	 	$zzz1=mysql_query($zzz);
     	 	if(mysql_num_rows($zzz1)>0)
     	 	{
     	 		while($zzz2=mysql_fetch_assoc($zzz1))
     	 		 {
     	 		 	     	 		 	$idr=$zzz2['id'];
     	 		 	     	 		 	$mmid=$zzz2['memid'];
     	 		 	     	 		 	$dbts=$zzz2['dbt'];
     	 		 	     	 		 	$crds=$crds+$dbts;
     	 		 	     	 		 	
     	 		$rrrr="UPDATE member_point_table SET `pt_status`='y' WHERE id='$idr' AND `memid`='$mmid'";
     	 		mysql_query($rrrr);
     	 		 	}
     	 		 	     	 		 	
     	 		 	}     	 		
     	 		
   
		$tot=1000;
		if($crds!=0)
		{
			$tot=1000+$crds;
			}
			if($cdd!=0)
			{
							$tot=$tot+$cdd;
							$crds=$crds+$cdd;
				}
		$Select_code91="SELECT *  FROM `member_point_table` WHERE  id='$gid'";
		$Select_code_res91=mysql_query($Select_code91) or die ("Query Failed credit.." .mysql_error());
		while($rw91=mysql_fetch_assoc($Select_code_res91))
			{
				$mem=$rw91['memid'];
     	 		 	$abc="SELECT * FROM member_registration WHERE `memberId`='$mem'";
     	 		 	             $abc111=mysql_query($abc) or die("InsertQuery Failed:".mysql_error());
     	 		 	while($row1111=mysql_fetch_assoc($abc111))
             {
             	
             if($row1111['sponsorId']=="0") 
             {
            $dbt=0;
          	}
     	 		else {
						$dbt=round($tot*25/100);
     	 			}
		
}
	}		
	
					//	$dbt=round($tot*25/100);
			
					
			$less=$tot-$dbt;
			$schg=round($less*2/100);
			$gross=$less-$schg;
			$tds=round($gross*10/100);
			$net=$gross-$tds;     	 		
     	 		
      	 		$exe="UPDATE member_point_table SET `pointachieve`='Y',`totalpoint`='1000',`achieve_date`='$current_date',crd='$crds',tot='$tot',dbt='$dbt',less='$less',schg='$schg',gross='$gross',tds='$tds',net='$net' WHERE id='$gid'";
     	 		mysql_query($exe);
     	 		 
     	 
     	 		 	
     	 		 	
     	 		 
     	 		 $k++;
     	 		 $gid++;
     	 		}
    
     	 	}
     	 	}


 ?>