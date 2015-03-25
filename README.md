# new_shape
作业   计算面积 周长
<?php 

// 体积 volume      表面积  superficial-area 
	abstract class shape{
		protected $mark1;  // 1是正方形,0是长方形r
		protected $r;
		protected static  $mianji;
		protected static  $zhouchang;
		protected static  $biaomianji;
		protected static  $tiji;
		const PI = M_PI;
		protected abstract function mianji();
		protected abstract function zhouchang();
	}

	interface tiji{
		
		function countTiji();  //不用x写abstract
	}

	interface biaomianji{
		
		function countBiaomianji();
	}

	class circle extends shape{    
	/**
	继承之后，$mianji 和 shape::$mianji 都能用，但指的不是同一个
	*/
		function __construct($mark,$r){
			$this->mark1 = $mark;
			$this->r = $r;
			if($this->mark1 != 0)
			{
				echo "这不是一个圆！";
			}
			if($this->mark1 ==0)
			{
				$this->mianji();
				$this->zhouchang();
			}
			
		}
		protected function mianji(){
			shape::$mianji = shape::PI*$this->r*$this->r;
			echo "园形面积:".shape::$mianji.",";
			
		}
		protected function zhouchang(){
			shape::$zhouchang = 2*$this->r*shape::PI;
			echo "园形周长:".shape::$zhouchang.",";
			
		}

	}

	class rectangle extends shape{
		function __construct($mark,$r){
			$this->mark1 = $mark;
			$this->r = $r;
			if($this->mark1 ==1)
			{
				$this->mianji();
				$this->zhouchang();
			}
			if($this->mark1 !=1){
				echo "这不是正方形！";
			}
		}
		protected function mianji(){
			shape::$mianji = $this->r * $this->r;
			echo "正方形面积:".shape::$mianji.",";
		}
		protected function zhouchang(){
			shape::$zhouchang = $this->r * 4;
			echo "正方形周长:".shape::$zhouchang.",";
		}
	}

	class cube extends rectangle implements tiji,biaomianji {   //正方体
		function __construct($a,$b){
			rectangle::__construct($a,$b);
			$this->countBiaomianji();
			$this->countTiji();
		}
		function countBiaomianji(){ 
			shape::$biaomianji = (shape::$mianji)*6;
			echo "正方体表面积:".shape::$biaomianji.","; 
		}
		function countTiji(){
			shape::$tiji = ($this->r)*($this->r)*($this->r);
			echo "正方体体积:".shape::$tiji."<br>";
		}
		
		

	}

	class sphere extends circle implements tiji,biaomianji{   //球
		function __construct($a,$b){
			circle::__construct($a,$b);
			$this->countBiaomianji();
			$this->countTiji();
		}
		function countBiaomianji(){
			shape::$biaomianji = 4*shape::$mianji;
			echo "球表面积:".shape::$biaomianji.","; 
		}
		function countTiji(){
			shape::$tiji = 4*shape::$mianji*$this->r/3;
			echo "球体积是:".shape::$tiji."<br>"; 
		}
		
		
	}

//	第一个参数传"0"表示圆形，"1"表示正方形；
//	第二个参数传半径或边长；
	$a = new rectangle(1,1);
	echo "<br>";
	$b = new sphere(0,2);


/*	class eee{
		const PI=3.14;
		function __construct(){
			$this->say();
		}
		public function say(){
			echo eee::PI;
	}
	}


	$e = new eee();
*/

	

?>
