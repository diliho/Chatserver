# -- 1. user表
CREATE TABLE `user` (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(50) NOT NULL,
    state ENUM('online', 'offline') DEFAULT 'offline'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

# -- 2. friend表
CREATE TABLE friend (
    userid INT NOT NULL,
    friendid INT NOT NULL,
    PRIMARY KEY (userid, friendid)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

# -- 3. all_group表
CREATE TABLE all_group (
    id INT PRIMARY KEY AUTO_INCREMENT,
    groupname VARCHAR(50) NOT NULL,
    groupdesc VARCHAR(200) DEFAULT ''
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

# -- 4. group_user表
CREATE TABLE group_user (
    groupid INT NOT NULL,
    userid INT NOT NULL,
    grouprole ENUM('creator', 'normal') DEFAULT 'normal',
    PRIMARY KEY (groupid, userid)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

# -- 5. offline_message表
CREATE TABLE offline_message (
    id INT PRIMARY KEY AUTO_INCREMENT,
    message VARCHAR(500) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;