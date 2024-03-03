
# Overview
`Siap Belajar?`  is a web-based application developed with HTML, CSS, JavaScript, PHP, and SQL. 

**Link to the video:** [click here.](https://drive.google.com/drive/folders/1DbgUdRfMfaY2pQYkXlvbrAIiPo_PxztZ?usp=sharing)

# Database Schema Tables

### Users Table
| Column Name | Data Type                 | Constraints                |
|-------------|---------------------------|----------------------------|
| user_id     | INT                       | PRIMARY KEY, AUTO_INCREMENT|
| email       | VARCHAR(255)              | UNIQUE, NOT NULL           |
| username    | VARCHAR(50)               | UNIQUE, NOT NULL           |
| password    | VARCHAR(255)              | NOT NULL                   |
| role        | ENUM('guru', 'siswa', 'admin') | NOT NULL               |

### Modul Table
| Column Name | Data Type                 | Constraints                |
|-------------|---------------------------|----------------------------|
| modul_id    | INT                       | PRIMARY KEY, AUTO_INCREMENT|
| nama_modul  | VARCHAR(100)              | NOT NULL                   |

### Jenjang Table
| Column Name | Data Type                 | Constraints                |
|-------------|---------------------------|----------------------------|
| jenjang_id  | INT                       | PRIMARY KEY, AUTO_INCREMENT|
| nama_jenjang| VARCHAR(20)               | NOT NULL                   |

### Isi_Modul Table
| Column Name | Data Type                 | Constraints                |
|-------------|---------------------------|----------------------------|
| isi_modul_id| INT                       | PRIMARY KEY, AUTO_INCREMENT|
| modul_id    | INT                       |                            |
| jenjang_id  | INT                       |                            |
| isi         | TEXT                      | NOT NULL                   |
| Foreign Keys| modul_id -> Modul(modul_id), jenjang_id -> Jenjang(jenjang_id)|

### Tes_Diagnostik Table
| Column Name | Data Type                 | Constraints                |
|-------------|---------------------------|----------------------------|
| tes_id      | INT                       | PRIMARY KEY, AUTO_INCREMENT|
| siswa_id    | INT                       |                            |
| modul_id    | INT                       |                            |
| hasil       | TEXT                      |                            |
| Foreign Keys| siswa_id -> Users(user_id), modul_id -> Modul(modul_id) |

### Tes_Modul Table
| Column Name | Data Type                 | Constraints                |
|-------------|---------------------------|----------------------------|
| tes_id      | INT                       | PRIMARY KEY, AUTO_INCREMENT|
| siswa_id    | INT                       |                            |
| modul_id    | INT                       |                            |
| hasil       | TEXT                      |                            |
| Foreign Keys| siswa_id -> Users(user_id), modul_id -> Modul(modul_id) |


# Database Schema Codes

```
CREATE TABLE Users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(255) UNIQUE NOT NULL,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('guru', 'siswa', 'admin') NOT NULL
);
```
```
CREATE TABLE Modul (
    modul_id INT PRIMARY KEY AUTO_INCREMENT,
    nama_modul VARCHAR(100) NOT NULL
);
```
```
CREATE TABLE Jenjang (
    jenjang_id INT PRIMARY KEY AUTO_INCREMENT,
    nama_jenjang VARCHAR(20) NOT NULL
);
```
```
CREATE TABLE Isi_Modul (
    isi_modul_id INT PRIMARY KEY AUTO_INCREMENT,
    modul_id INT,
    jenjang_id INT,
    isi TEXT NOT NULL,
    FOREIGN KEY (modul_id) REFERENCES Modul(modul_id),
    FOREIGN KEY (jenjang_id) REFERENCES Jenjang(jenjang_id)
);
```
```
CREATE TABLE Tes_Diagnostik (
    tes_id INT PRIMARY KEY AUTO_INCREMENT,
    siswa_id INT,
    modul_id INT,
    hasil TEXT,
    FOREIGN KEY (siswa_id) REFERENCES Users(user_id),
    FOREIGN KEY (modul_id) REFERENCES Modul(modul_id)
);
```
```
CREATE TABLE Tes_Modul (
    tes_id INT PRIMARY KEY AUTO_INCREMENT,
    siswa_id INT,
    modul_id INT,
    hasil TEXT,
    FOREIGN KEY (siswa_id) REFERENCES Users(user_id),
    FOREIGN KEY (modul_id) REFERENCES Modul(modul_id)
);
```
