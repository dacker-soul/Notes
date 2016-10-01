function:打乱一维数组
--------------------

function shuffle_assoc($list) {   
  if (!is_array($list)) return $list;   
  $keys = array_keys($list);   
  shuffle($keys);   
  $random = array();   
  foreach ($keys as $key)   
    $random[$key] = $list[$key];   
  return $random;   
}


function:打乱多维数组
--------------------

function rec_assoc_shuffle($array){  
  $ary_keys = array_keys($array);  
  $ary_values = array_values($array);  
  shuffle($ary_values);  
  foreach($ary_keys as $key => $value) {  
    if (is_array($ary_values[$key]) AND $ary_values[$key] != NULL) {  
      $ary_values[$key] = rec_assoc_shuffle($ary_values[$key]);  
    }  
    $new[$value] = $ary_values[$key];  
  }  
  return $new;  
}


function:判断是否是ajax请求
-------------------------

public static function is_ajax_request(){
  if (isset($_SERVER['HTTP_X_REQUESTED_WITH']) && strtolower($_SERVER['HTTP_X_REQUESTED_WITH']) == 'xmlhttprequest') {
      return 1;
  } else {
      return 2;
  }
}


function:日期时间处理
--------------------

public function show_time($show_time){
    if(strlen($show_time) == 19){
        $show_time = strtotime($show_time);
    }
    $dur = time() - $show_time;
    if($dur <=0){
        return '0秒前';
    }else{
        if($dur < 60){
            return $dur.'秒前';
        }else{
            if($dur < 3600){
                return floor($dur/60).'分钟前';
            }else{
                $current_time = date("Y-m-d",time());
                $date = date("Y-m-d",$show_time);
                if($current_time == $date){
                    return "今天 ".date("H:i",$show_time);
                }else{
                    $current_year = date("Y",time());
                    $year = date("Y",$show_time);
                    if($current_year == $year){//一年内
                        return date("m-d H:i",$show_time);
                    }else{
                        return date("Y-m-d H:i",$show_time);
                    }
                }
            }
        }
    }
  }
    

function:正则密码（至少一个大写字母，一个小写字母，一个数字，一个特殊符号，6-16位）
----------------------------------------------------------------------------
public function checkPassword(){
  $subject = 'Ly44444@';
  if(preg_match('/(?=.*[0-9])(?=.*[a-z])(?=.*[!@#$%^&*])(?=.*[A-Z]).{6,16}/',$subject)){
      echo 'gg';die();
  }
}
