#
                                                        ==================================================
                                                                        ប្រព័ន្ធគ្រប់គ្រងចងការប្រាក់
                                                        ==================================================

# នៅក្នុងប្រព័ន្ធគ្រប់គ្រងនេះមានមុខងារដូចជា​
==================================

  # លីញតំណរ
    - UI: Figma Design (Link): https://www.figma.com/design/Adfpwx2gltAFuJAmlzsfaw/System-loan?node-id=0-1&p=f&t=Jf11vn8jHV5y8H6P-0
    - Demo : Web Design (Link): 
    - Database: On Below (Note)
    - Test: System Loan (Link):
                                                        ==================================================

  # Font, Font Size, Colors
    - Khmer font name: Dangrek:font-family: "Dangrek", sans-serif; and Bokor: font-family: "Bokor", system-ui;
    - Font size: 12px, 14px, 16px, 20px, 24px, 28px, 32px, 35px, 45px
    - Colors: Border-color: #D1D5DB; Text-color: #4B5563; Background: #FFFFFF; Active: #0D9488;

  # Link Google font: 
      @import url('<https://fonts.googleapis.com/css2?family=Audiowide&family=Bokor&family=Bungee&family=Dangrek&family=Fugaz+One&family=JetBrains+Mono:ital,wght@0,100..800;1,100..800&family=Lilita+One&family=Permanent+Marker&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Prompt:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&family=Russo+One&family=Spicy+Rice&display=swap>');

                                                        =================================================

  # នៅក្នុងទំព័រដើមមានបង្ហាញនៅផ្ទាំងជាច្រើនដូចជា: 
    - ប្រាក់ចំណូលទាំងអស់ 
    - ចំនួនអតិថិជនសរុប
    - អតិថិជនដែលបានបកប្រាក់កម្ចីសរុប
    - អតិថិជនដែលចងការប្រាក់ច្រើនបំផុត​ 
    - របាយការណ៍សរុប 
    - និង Chart។
    
  # ក្នុងប្រព័ន្ធនេះគឺមានមុខងារច្រើនដូចជា: 
    - ការបង្កើតនិងចែ ឬ​ ចុះឈ្មោះរបស់អតិថិជនចូលក្នុងប្រព័ន្ធ
    -​ ការបង្កើតការចងការប្រាក់របស់អតិថិជនក្នុងប្រព័ន្ធ
    - ការឡើងការប្រាប់ប្រចាំថ្ងៃ
    - ការបកប្រាក់កម្ចីរបស់ធតិថិជន
    - Chart
    - ការបង្ហាញទិន្នន័យតាមលេខទំព័រ
    - បញ្ចូលរូបភាពនិងវិដេអូ
    - ប្រើបានគ្រប់ប្រភេទ។

  # This fields and tables of system loan.
    - CREATE TABLE clients (
        id INT PRIMARY KEY AUTO_INCREMENT,
        fullName VARCHAR(100) NOT NULL,
        gender ENUM('Male', 'Female', 'Other'),
        phoneNumber VARCHAR(20),
        address TEXT,
        id_card VARCHAR(50) UNIQUE,
        profile TEXT
    );

    - CREATE TABLE loans (
        id INT PRIMARY KEY AUTO_INCREMENT,
        id_client INT,
        loan_Amount DECIMAL(12,2) NOT NULL,
        interest_Rate DECIMAL(5,2) NOT NULL,
        loan_Term INT, -- in months or days, depending on your needs
        payment_Amount DECIMAL(12,2),
        start_Date DATE,
        picture VARCHAR(255), -- path to picture file
        video VARCHAR(255), -- path to video file
        status ENUM('Active', 'Completed', 'Defaulted', 'Pending') DEFAULT 'Pending',
        FOREIGN KEY (id_client) REFERENCES clients(id)
    );

    - CREATE TABLE payments (
        id INT PRIMARY KEY AUTO_INCREMENT,
        id_loan INT,
        payment_Amount DECIMAL(12,2) NOT NULL,
        not_paid DECIMAL(12,2) DEFAULT 0.00,
        payment_date DATE,
        payment_Status ENUM('Paid', 'Pending', 'Late') DEFAULT 'Pending',
        FOREIGN KEY (id_loan) REFERENCES loans(id)
    );

    - CREATE TABLE return_loan (
        id INT PRIMARY KEY AUTO_INCREMENT,
        id_loan INT,
        day_left INT, (tngai nv sol)
        money_left INT, (luy nv sol)
        more_money DECIMAL(12,2), (p'krub luy)
        start_Date DATE, (new loan)
        status ENUM('Active', 'Completed', 'Overdue') DEFAULT 'Active',
        FOREIGN KEY (id_loan) REFERENCES loans(id)
    );

    - CREATE TABLE profit (
        id INT PRIMARY KEY AUTO_INCREMENT,
        id_loan INT,
        profit DECIMAL(12,2),
        FOREIGN KEY (id_loan) REFERENCES loans(id)
    );

    - CREATE TABLE end_paid (
        id INT PRIMARY KEY AUTO_INCREMENT,
        id_loan INT,
        status ENUM('Paid', 'Pending') DEFAULT 'Pending',
        FOREIGN KEY (id_loan) REFERENCES loans(id)
    );