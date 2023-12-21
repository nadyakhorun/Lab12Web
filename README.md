# Lab12Web

Nama            : Nadya Khairunnisa

NIM             : 312210133

Kelas           : TI.22.A.1

Mata Kuliah     : Pemrograman Web 1

Dosen Pengampu  : Agung Nugroho, S.Kom., M.Kom

# Praktikum: PHP dan MySQL Database

# Studi Kasus: Login Form

# DDL: Table user

      CREATE TABLE `user`(
            `id` INT NOT NULL AUTO_INCREMENT,
            `username` VARCHAR(50),
            `password` VARCHAR(50),
            PRIMARY KEY (`id`),
            UNIQUE INDEX `UNIQUE` (`username`)
      ) ENGINE=MYISAM;
      INSERT INTO `user` (`username`, `password`) VALUES ('admin', md5('admin'));

# File: login_session.php

Deskripsi: dignakan untuk pengecekan sesi login, file ini nantinya akan di include disetiap halaman yang membutuhkan login.

        <?php
        session_start();
        if (!isset($_SESSION['isLogin']))
        header('location: login.php');
        ?>

# File: login.php

              <?php
              session_start();
              $title = 'Data Barang';
              include_once 'koneksi.php';
              if (isset($_POST['submit']))
              {
              $user = $_POST['user'];
              $password = $_POST['password'];
              $sql = "SELECT * FROM user WHERE username = '{$user}'
              AND password = md5('{$password}') ";
              $result = mysqli_query($conn, $sql);
              if ($result && mysqli_affected_rows($conn) != 0)
              {
              $_SESSION['isLogin'] = true;
              $_SESSION['user'] = mysqli_fetch_array($result);
              header('location: index.php');
              } else
              $errorMsg = "<p style=\"color:red;\">Gagal Login,silakan ulangi lagi.</p>";
              }
              include_once "header.php";
              if (isset($errorMsg)) echo $errorMsg;
              ?>
              <h2>Login</h2>
              <form method="post">
              <div class="input">
              <label>Username</label>
              <input type="text" name="user" />
              </div>
              <div class="input">
              <label>Password</label>
              <input type="password" name="password" />
              </div>
              <div class="submit">
              <input type="submit" name="submit" value="Login" />
              </div>
              </form>
              <?php
              include_once 'footer.php';
              ?>
