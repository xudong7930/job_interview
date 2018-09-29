适配器模式(adapter)
=======================

> 将一个类的接口，转换成客户期望的另一个类的接口。适配器让原本接口不兼容的类可以合作无间

```php
interface Target
{
    public function connect($host,$user,$passwd,$dbname);
    public function query($sql);
    public function close();
}

class MySQLAdapter implements Target
{
    protected $conn;

    public function connect($host, $user, $passwd, $dbname)
    {
        $conn = mysql_connect($host,$user, $passwd);
        mysql_select_db($dbname, $conn);
        $this->conn = $conn;
    }

    public function query($sql)
    {
        return mysql_query($sql, $this->conn);
    }

    public function close()
    {
        mysql_close($this->conn);
    }
}

class MySQLiAdapter implements Target
{
    protected $conn;

    public function connect($host, $user, $passwd, $dbname)
    {
        $conn = mysqli_connect($host, $user, $passwd);
        mysqli_select_db($dbname, $conn);
        $this->conn = $conn;
    }
    public function query($sql)
    {
        return mysqli_query($sql, $this->conn);
    }

    public function close()
    {
        mysqli_close($this->conn);
    }
}

class DataBase implements Target
{
    protected $db;
    public function __construct($type)
    {
        $type = $type.'Adapter';
        $this->db = new $type;
    }

    public function connect($host, $user, $passwd, $dbname)
    {
        $this->db->connect($host, $user, $passwd, $dbname);
    }
    public function query($sql)
    {
        return $this->db->query($sql);
    }

    public function close()
    {
        $this->db->close();
    }
}

$db1 = new DataBase('MySQL');
$db1->connect('127.0.0.1', 'root','root','myDB');
$db1->query('select * from test');
$db1->close();

$db2 = new DataBase('MySQLi');
$db2->connect('127.0.0.1', 'root','root','myDB');
$db2->query('select * from test');
$db2->close();
```