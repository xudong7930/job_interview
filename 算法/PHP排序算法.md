PHP排序算法
==========

## 测试数组
```php
$arr1 = [11, -3, 57,11, -7, 9, 100, 2, -56, 32, 21];

echo implode(',', insertSort($arr)).PHP_EOL;
echo implode(',', selectSort($arr)).PHP_EOL;
echo implode(',', bublleSort($arr)).PHP_EOL;
echo implode(',', quickSort($arr)).PHP_EOL;
```

## 插入排序
```php
function insertSort($arr)
{
    $len = count($arr);

    for($i=1; $i<$len; $i++) {
        $tmp = $arr[$i];

        for($j=$i-1; $j>=0; $j--) {
            if ($tmp > $arr[$j]) {
                break;
            }

            $arr[$j + 1] = $arr[$j];
            $arr[$j] = $tmp;
        }
    }

    return $arr;
}
```

## 选择排序
```php
function selectSort($arr)
{
    $len = count($arr);
    for($i=0;$i<$len-1; $i++) {
        $p = $i;

        for($j=$i+1; $j<$len; $j++) {
            if($arr[$p] > $arr[$j]){
                $p = $j;
            }
        }

        if($p != $i){
            $tmp = $arr[$p];
            $arr[$p] = $arr[$i];
            $arr[$i] = $tmp;
        }
    }

    return $arr;
}
```

## 冒泡排序
```php
function bublleSort($arr)
{
    $len = count($arr);

    for($i=1;$i<$len;$i++){
        for($j=0;$j<$len-$i;$j++) {
            if ($arr[$j] > $arr[$j + 1]) {
                $tmp = $arr[$j + 1];
                $arr[$j + 1] = $arr[$j];
                $arr[$j] = $tmp;
            }
        }
    }

    return $arr;
}
```

## 快速排序
```php
function quickSort($arr)
{
    $len = count($arr);
    
    if( $len<2 ) {
        return $arr;
    }

    $middle = $arr[0];
    $left = [];
    $right = [];

    for($i=1; $i<$len; $i++){
        if($middle > $arr[$i]){
            $left[] = $arr[$i];
        } else {
            $right[] = $arr[$i];
        }
    }

    $left = quickSort($left);
    $right = quickSort($right);
    return array_merge($left, [$middle], $right);
}
```