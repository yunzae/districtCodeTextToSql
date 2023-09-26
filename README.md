# districtCodeTextToSql
대한민국 법정동 코드를 DB에 넣기 위한 sql변환기




데이터 베이스 구조: 시도-시구군(일대다), 시구군-읍면동(일대다)

       CREATE TABLE IF NOT EXISTS city_tb (
            id INT AUTO_INCREMENT PRIMARY KEY,
            name VARCHAR(255) UNIQUE NOT NULL
        );
        
       CREATE TABLE IF NOT EXISTS country_tb (
            id INT AUTO_INCREMENT PRIMARY KEY,
            city_id INT,
            name VARCHAR(255) NOT NULL,
            FOREIGN KEY (city_id) REFERENCES city_tb(id),
            CONSTRAINT unique_city_name UNIQUE (city_id, name) 
        );
        
        CREATE TABLE IF NOT EXISTS district_tb (
            id INT AUTO_INCREMENT PRIMARY KEY,
            statutory_code BIGINT UNIQUE NOT NULL,
            country_id INT,
            name VARCHAR(255) NOT NULL,
            FOREIGN KEY (country_id) REFERENCES country_tb(id),
            CONSTRAINT unique_country_name UNIQUE (country_id, name)
        );
