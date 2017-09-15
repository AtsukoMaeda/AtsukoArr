# AtsukoArr
PHP数组处理
$a=new AtsukoArr($arr);
where
$a->where($where)
查找方法，$where可以是数组也可以是字符串，数组以['id'=>1,'name'=>'atsuko'...]格式，字符串如果有in查询，in查询格式为'id in(1,2,6,4)'，in查询后面可以跟对比查询，用and连接，如'id in(1,2,3,4,5) and age>14 and age<25'，notin用法同in，如果需要多个and可以用数组['id'=>1,'name'=>'atsuko'...]，支持or查询，支持like查询

order
$a->order($order)
排序方法，$order可以是数组也可以是字符串，数组以['id'=>'desc','age'=>'asc',...]格式，
字符串如'id desc'，有多个排序规则以逗号隔开如'id desc,age asc'

setInc
$a->setInc($field,$int='')
键加方法，如果没有$int，则结果集内对应的$field数值+1，如果$int有值，则+$int，其中，field可以是字符串如'age','age,height'，
也可以是数组['age'],['age','height']，这些键都是同时加，如果想不同的键加不同的值，可重复调用该方法

setDec
$a->setDec($field,$int='')
键减方法，如果没有$int，则结果集内对应的$field数值-1，如果$int有值，则-$int，其中，field可以是字符串如'age','age,height'，
也可以是数组['age'],['age','height']，这些键都是同时减，如果想不同的键减不同的值，可重复调用该方法

field
$a->field($field)
限定键方法，$field可以是数组也可以是字符串，使用该方法之后得出的结果集只会包含$filed的键，该方法后面不能调用delete方法

select
$a->select()
返回处理后的数组

find
$a->find($id='')
返回结果集，$id如果没有值返回一维数组，不管满足条件的的有多少只返回第一条，若$id有值，则返回对应顺序的结果

setField
$a->setField($key,$value='',$flag=false)
给得出的结果集的对应键设定值，一次修改一个键setField('name','aaa')，一次修改多个键，setField(['name'=>'heeh','age'=>16])，
如果得出的结果多并且想全部都修改，在后面加个true，setField('name','aaa',true),setField(['name'=>'heeh','age'=>16],true)

getField
$a->getField($field,$flag=false)
返回需要的键的值，返回一个键getField('name')，此时返回的是字符串，返回多个键getField('name,age')，getField(['name','age'])，
此时返回一维数组，如果想获得多个，getField('name',true)，返回一维数组，getField('name,age',true)，getField(['name','age'],true)，
返回二维数组，同时若$flag输入的是数字，也返回多个，不过是$flag个

add
$a->add($arr,$type=true)
往数组内再添加数组，可以是一维数组，也可以是二维数组，该方法会自动判定加入的数组的键是否是处理数组内有的，有的才会加入，
若增加的数组里面没有一个键是对应的，则不添加，若有至少一个键是对应的，则根据$type的值有两种情况，
$type默认是如果增加的数组有些键没值，给空值，$type为false则如果有些键没值则整个不加入

delete
$a->delete($id=null)
从处理的数组中删除满足条件的数组，得到剩下的数组，该方法前面不可使用field方法，如果$id有值，则会在原数组中删除对应的第几个数组，
$id可以是数字1，字符串'1,3'，数组[1,3]，再返回剩下的

uniq
$a->uniq($field='')
去重复的数组，用于二维数组中，如果$field没值，则二维数组中完全一样的索引靠后的会被去重，如果$field有值，该值可以是字符串也可以是数组，
如uniq('name')，uniq('name,age')，uniq(['name'])，uniq(['name','age'])，这时只要该键一样就去重

sortOut
$a->sortOut($arr='')
分散数组整理，如['id'=>[1,2,3],'name'=>['a','b','c']]整理成[['id'=>1,'name'=>'a'],['id'=>2,'name'=>'b'],['id'=>3,'name'=>'c'],]，
如果$arr有值，则处理后返回，如果$arr无值，则处理实例化输入的那个数组，不返回值

limit
$a->limit($limit)
截取返回的结果集，如果$limit是单个数字，则从结果集中从最前的返回$limit个结果，如果类似'1,5'，则从1号开始一共返回5个

count
$a->count()
返回结果集的数量

setKeys
$a->setKeys($keys,$newkeys='')
修改数组内的键名，输入两个参数的时候修改一个键名，输入一个参数且为数组则可修改多个键名

end
$a->end()
返回原数组，将处理数组返回最初状态

vkSort
$a->vkSort($arr=false,$order='v desc,k desc')
返回处理后的数组，输入为一维数组，第二个参数是排序规则，可以按照一维数组的键和值来排序

change
$a->change($arr)
重新设定处理数组，该设定同时影响end返回数组

arrGetAll
$a->arrGetAll($arr)
给定分开的数组，得出所有组合，如$arr=['品牌'=>['索尼','联想'],'尺寸'=>[18]]，得出$return=[[品牌=>'索尼','尺寸'=>18],['品牌'=>'联想','尺寸'=>18]]