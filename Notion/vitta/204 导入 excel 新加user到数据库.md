<!DOCTYPE html PUBLIC “-//W3C//DTD XHTML 1.0 Transitional//EN” “http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd”>

  

1. 在 `dev.php` 中：

```Plain
 public function __construct($need_login = false, $theme = ’md’)
    {
        parent::__construct($need_login, $theme);

        if (!$this->input->cookie(DEBUG_COOKIE)) {
            die(‘Access denied!’);
        }

        $this->load->model(‘employee’);
    }
```

```Plain
     public function import_new_drivers() {
        $this->load->library("ExcelParser");
        $obj = ExcelParser::phpexcel_import(DIR . ’/../../tmp/TDL_Kristiansand_Drivers.xlsx’);
        $rows = $obj[’20180701(2)‘];
        foreach ($rows as $row) {
            $employ_no = $row[’Employee number’];
            $firstName = $row[’First name’];
            $lastName = $row[’Last name’];

            if (!$this->employee->get($employ_no)) {
                $this->db->insert(‘br_employee’, array(
                    ’em_id’ => $employ_no,
                    ’name’ => $row[’First name’] . ’, ’ . $row[’Last name’],
                    ’phone’ => $row[’Phone number’],
                    ’cellphone’ => $row[’Phone number’],
                    ’mail’ => $row[’Email’],
                ));
                echo $this->db->last_query() . ’;<br/>’;
            }

            $username = mb_substr($firstName, 0, 1) .
                        mb_substr($lastName, 0, 1) .
                        $employ_no;

            if ($this->user->get_info_by_username($username)) {
                var_dump($username);
                continue;
            }

            $this->db->insert(‘br_users’, array(
                ’employe_no’ => $employ_no,
                ’username’ => $username,
                ’password’ => md5($employ_no),
                ’firstname’ => $firstName,
                ’lastname’ => $lastName,
                ’office_phone’ => $row[’Phone number’],
                ’cell_phone’ => $row[’Phone number’],
                ’expiry’ => 2074197600,
                ’email’ => $row[’Email’],
                ’depot_id’ => 53, // Kristiansand
                ’worklocation_en’ => ’Kristiansand’,
                ’worklocation_nov’ => ’Kristiansand’,
            ));
            echo $this->db->last_query() . ’;<br/>’;
            $id = $this->db->insert_id();

            $this->db->insert(‘br_users_roles’, array(
                ’user_id’ => $id,
                ’loc_id’ => 0,
                ’loc_ids’ => ’all’,
                ’home’ => 1,
                ’role_id’ => 46,
                ’start_date’ => 1455750000,
                ’end_date’ => 2043180000,
                ’defaulted’ => 1
            ));
            echo $this->db->last_query() . ’;<br/>’;
        }
    }
```