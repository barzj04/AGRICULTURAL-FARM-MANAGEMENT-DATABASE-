CREATION OF TABLES

-- Create OWNER table
CREATE TABLE OWNER (
    OwnerID INT PRIMARY KEY,
    FName VARCHAR(100),
    LName VARCHAR(100),
    CInfo VARCHAR(100)
);

-- Create FARM table
CREATE TABLE FARM (
    FarmID INT PRIMARY KEY,
    FarmName VARCHAR(100),
    Location VARCHAR(100),
    FSize DECIMAL(10, 2),
    OwnerID INT,
    FOREIGN KEY (OwnerID) REFERENCES OWNER(OwnerID)
);

-- Create FIELD table
CREATE TABLE FIELD (
    FieldID INT PRIMARY KEY,
    FarmID INT,
    FieldName VARCHAR(100),
    FArea DECIMAL(10, 2),
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);

-- Create CROP table
CREATE TABLE CROP (
    CropID INT PRIMARY KEY,
    FieldID INT,
    CropType VARCHAR(100),
    CPlantingDate DATE,
    CHarvestDate DATE,
    FOREIGN KEY (FieldID) REFERENCES FIELD(FieldID)
);

-- Create PESTICIDE table
CREATE TABLE PESTICIDE (
    PesticideID INT PRIMARY KEY,
    PesticideName VARCHAR(100),
    PApplicationDate DATE,
    Dosage VARCHAR(100)
);

-- Create PEST table
CREATE TABLE PEST (
    PestID INT PRIMARY KEY,
    CropID INT,
    PestType VARCHAR(100),
    PDetectedDate DATE,
    PesticideID INT,
    FOREIGN KEY (CropID) REFERENCES CROP(CropID),
    FOREIGN KEY (PesticideID) REFERENCES PESTICIDE(PesticideID)
);

-- Create LIVESTOCK table
CREATE TABLE LIVESTOCK (
    LivestockID INT PRIMARY KEY,
    FarmID INT,
    AType VARCHAR(100),
    LBirthDate DATE,
    HealthStatus VARCHAR(100),
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);

-- Create EQUIPMENT table
CREATE TABLE EQUIPMENT (
    EquipmentID INT PRIMARY KEY,
    FarmID INT,
    EName VARCHAR(100),
    EType VARCHAR(100),
    EPurchaseDate DATE,
    MaintenanceSchedule VARCHAR(100),
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);

-- Create WORKER table
CREATE TABLE WORKER (
    WorkerID INT PRIMARY KEY,
    FarmID INT,
    FirstName VARCHAR(100),
    LastName VARCHAR(100),
    Role VARCHAR(100),
    ContactInfo VARCHAR(100),
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);

-- Create TASK table
CREATE TABLE TASK (
    TaskID INT PRIMARY KEY,
    FieldID INT,
    CropID INT,
    LivestockID INT,
    Description VARCHAR(255),
    WorkerID INT,
    TDueDate DATE,
    Status VARCHAR(100),
    FOREIGN KEY (FieldID) REFERENCES FIELD(FieldID),
    FOREIGN KEY (CropID) REFERENCES CROP(CropID),
    FOREIGN KEY (LivestockID) REFERENCES LIVESTOCK(LivestockID),
    FOREIGN KEY (WorkerID) REFERENCES WORKER(WorkerID)
);

-- Create IRRIGATION_SYSTEM table
CREATE TABLE IRRIGATION_SYSTEM (
    IrrigationID INT PRIMARY KEY,
    FieldID INT,
    IInstallationDate DATE,
    ICapacity DECIMAL(10, 2),
    FOREIGN KEY (FieldID) REFERENCES FIELD(FieldID)
);

-- Create WEATHER table
CREATE TABLE WEATHER (
    WeatherID INT PRIMARY KEY,
    FieldID INT,
    WDate DATE,
    Temperature DECIMAL(5, 2),
    Rainfall DECIMAL(5, 2),
    Humidity DECIMAL(5, 2),
    FOREIGN KEY (FieldID) REFERENCES FIELD(FieldID)
);

-- Create HARVEST table
CREATE TABLE HARVEST (
    HarvestID INT PRIMARY KEY,
    CropID INT,
    HHarvestDate DATE,
    Quantity DECIMAL(10, 2),
    Quality VARCHAR(100),
    FOREIGN KEY (CropID) REFERENCES CROP(CropID)
);

-- Create BUYER table
CREATE TABLE BUYER (
    BuyerID INT PRIMARY KEY,
    BuyerName VARCHAR(100),
    ContactInfo VARCHAR(100)
);

-- Create SALE table
CREATE TABLE SALE (
    SaleID INT PRIMARY KEY,
    HarvestID INT,
    BuyerID INT,
    SDate DATE,
    Quantity DECIMAL(10, 2),
    Price DECIMAL(10, 2),
    FOREIGN KEY (HarvestID) REFERENCES HARVEST(HarvestID),
    FOREIGN KEY (BuyerID) REFERENCES BUYER(BuyerID)
);

-- Create STORAGE table
CREATE TABLE STORAGE (
    StorageID INT PRIMARY KEY,
    FarmID INT,
    StorageType VARCHAR(100),
    SCapacity DECIMAL(10, 2),
    Location VARCHAR(100),
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);

-- Create INVENTORY table
CREATE TABLE INVENTORY (
    InventoryID INT PRIMARY KEY,
    FarmID INT,
    ItemName VARCHAR(100),
    Quantity DECIMAL(10, 2),
    Unit VARCHAR(100),
    ILastUpdated DATE,
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);

-- Create VETERINARY table
CREATE TABLE VETERINARY (
    VetRecordID INT PRIMARY KEY,
    LivestockID INT,
    VVisitDate DATE,
    Treatment VARCHAR(255),
    Veterinarian VARCHAR(100),
    FOREIGN KEY (LivestockID) REFERENCES LIVESTOCK(LivestockID)
);

-- Create FINANCIAL_RECORD table
CREATE TABLE FINANCIAL_RECORD (
    FinanceID INT PRIMARY KEY,
    FarmID INT,
    RecordType VARCHAR(100),
    Amount DECIMAL(10, 2),
    FDate DATE,
    Description VARCHAR(255),
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);

-- Create MAINTENANCE_RECORD table
CREATE TABLE MAINTENANCE_RECORD (
    MaintenanceID INT PRIMARY KEY,
    EquipmentID INT,
    MDate DATE,
    Description VARCHAR(255),
    Cost DECIMAL(10, 2),
    FOREIGN KEY (EquipmentID) REFERENCES EQUIPMENT(EquipmentID)
);

-- Create TRAINING table
CREATE TABLE TRAINING (
    TrainingID INT PRIMARY KEY,
    FarmID INT,
    Topic VARCHAR(100),
    TDate DATE,
    Trainer VARCHAR(100),
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);

-- Create COMPLIANCE_RECORD table
CREATE TABLE COMPLIANCE_RECORD (
    ComplianceID INT PRIMARY KEY,
    FarmID INT,
    Regulation VARCHAR(100),
    CInspectionDate DATE,
    Status VARCHAR(100),
    FOREIGN KEY (FarmID) REFERENCES FARM(FarmID)
);




POPULATE TABLE WITH DATA


--- Before inserting data into OWNER table
SELECT * FROM OWNER;

-- Insert records into OWNER table
INSERT INTO OWNER (OwnerID, FName, LName, CInfo) VALUES (1, 'John', 'Doe', 'john.doe@gmail.com');
INSERT INTO OWNER (OwnerID, FName, LName, CInfo) VALUES (2, 'Jane', 'Smith', 'jane.smith@yahoo.com');
INSERT INTO OWNER (OwnerID, FName, LName, CInfo) VALUES (3, 'Alice', 'Johnson', 'alice.johnson@outlook.com');
INSERT INTO OWNER (OwnerID, FName, LName, CInfo) VALUES (4, 'Robert', 'Brown', 'robert.brown@gmail.com');
INSERT INTO OWNER (OwnerID, FName, LName, CInfo) VALUES (5, 'Maria', 'Garcia', 'maria.garcia@hotmail.com');

-- After inserting data into OWNER table
SELECT * FROM OWNER;

-- Before inserting data into FARM table
SELECT * FROM FARM;

-- Insert records into FARM table
INSERT INTO FARM (FarmID, FarmName, Location, FSize, OwnerID) VALUES (1, 'Green Acres', 'Springfield', 150.5, 1);
INSERT INTO FARM (FarmID, FarmName, Location, FSize, OwnerID) VALUES (2, 'Sunny Fields', 'Shelbyville', 200.0, 2);
INSERT INTO FARM (FarmID, FarmName, Location, FSize, OwnerID) VALUES (3, 'Happy Farm', 'Ogdenville', 120.0, 3);
INSERT INTO FARM (FarmID, FarmName, Location, FSize, OwnerID) VALUES (4, 'Farm Fresh', 'North Haverbrook', 180.0, 4);
INSERT INTO FARM (FarmID, FarmName, Location, FSize, OwnerID) VALUES (5, 'Golden Harvest', 'Capital City', 250.0, 5);

-- After inserting data into FARM table
SELECT * FROM FARM;

-- Before inserting data into FIELD table
SELECT * FROM FIELD;

-- Insert records into FIELD table
INSERT INTO FIELD (FieldID, FarmID, FieldName, FArea) VALUES (1, 1, 'Field A', 50.5);
INSERT INTO FIELD (FieldID, FarmID, FieldName, FArea) VALUES (2, 1, 'Field B', 60.0);
INSERT INTO FIELD (FieldID, FarmID, FieldName, FArea) VALUES (3, 2, 'Field C', 70.0);
INSERT INTO FIELD (FieldID, FarmID, FieldName, FArea) VALUES (4, 2, 'Field D', 80.0);
INSERT INTO FIELD (FieldID, FarmID, FieldName, FArea) VALUES (5, 3, 'Field E', 90.0);

-- After inserting data into FIELD table
SELECT * FROM FIELD;

-- Before inserting data into CROP table
SELECT * FROM CROP;

-- Insert records into CROP table
INSERT INTO CROP (CropID, FieldID, CropType, CPlantingDate, CHarvestDate) VALUES (1, 1, 'Wheat', DATE '2023-03-01', DATE '2023-07-15');
INSERT INTO CROP (CropID, FieldID, CropType, CPlantingDate, CHarvestDate) VALUES (2, 2, 'Corn', DATE '2023-04-01', DATE '2023-08-20');
INSERT INTO CROP (CropID, FieldID, CropType, CPlantingDate, CHarvestDate) VALUES (3, 3, 'Barley', DATE '2023-05-01', DATE '2023-09-25');
INSERT INTO CROP (CropID, FieldID, CropType, CPlantingDate, CHarvestDate) VALUES (4, 4, 'Soybeans', DATE '2023-06-01', DATE '2023-10-30');
INSERT INTO CROP (CropID, FieldID, CropType, CPlantingDate, CHarvestDate) VALUES (5, 5, 'Rice', DATE '2023-07-01', DATE '2023-11-15');

-- After inserting data into CROP table
SELECT * FROM CROP;

-- Before inserting data into PESTICIDE table
SELECT * FROM PESTICIDE;

-- Insert records into PESTICIDE table
INSERT INTO PESTICIDE (PesticideID, PesticideName, PApplicationDate, Dosage) VALUES (1, 'RoundUp', DATE '2023-05-15', '2L/ha');
INSERT INTO PESTICIDE (PesticideID, PesticideName, PApplicationDate, Dosage) VALUES (2, 'Sevin', DATE '2023-06-01', '1.5kg/ha');
INSERT INTO PESTICIDE (PesticideID, PesticideName, PApplicationDate, Dosage) VALUES (3, 'Malathion', DATE '2023-06-15', '1L/ha');
INSERT INTO PESTICIDE (PesticideID, PesticideName, PApplicationDate, Dosage) VALUES (4, 'Neem Oil', DATE '2023-07-01', '3L/ha');
INSERT INTO PESTICIDE (PesticideID, PesticideName, PApplicationDate, Dosage) VALUES (5, 'Bt spray', DATE '2023-07-15', '500g/ha');

-- After inserting data into PESTICIDE table
SELECT * FROM PESTICIDE;

-- Before inserting data into PEST table
SELECT * FROM PEST;

-- Insert records into PEST table
INSERT INTO PEST (PestID, CropID, PestType, PDetectedDate, PesticideID) VALUES (1, 1, 'Aphids', DATE '2023-05-10', 1);
INSERT INTO PEST (PestID, CropID, PestType, PDetectedDate, PesticideID) VALUES (2, 2, 'Corn Borer', DATE '2023-06-05', 2);
INSERT INTO PEST (PestID, CropID, PestType, PDetectedDate, PesticideID) VALUES (3, 3, 'Grasshoppers', DATE '2023-06-20', 3);
INSERT INTO PEST (PestID, CropID, PestType, PDetectedDate, PesticideID) VALUES (4, 4, 'Spider Mites', DATE '2023-07-05', 4);
INSERT INTO PEST (PestID, CropID, PestType, PDetectedDate, PesticideID) VALUES (5, 5, 'Rice Weevil', DATE '2023-07-20', 5);

-- After inserting data into PEST table
SELECT * FROM PEST;

-- Before inserting data into LIVESTOCK table
SELECT * FROM LIVESTOCK;

-- Insert records into LIVESTOCK table
INSERT INTO LIVESTOCK (LivestockID, FarmID, AType, LBirthDate, HealthStatus) VALUES (1, 1, 'Cattle', DATE '2021-01-15', 'Healthy');
INSERT INTO LIVESTOCK (LivestockID, FarmID, AType, LBirthDate, HealthStatus) VALUES (2, 1, 'Sheep', DATE '2021-02-20', 'Healthy');
INSERT INTO LIVESTOCK (LivestockID, FarmID, AType, LBirthDate, HealthStatus) VALUES (3, 2, 'Goat', DATE '2021-03-25', 'Healthy');
INSERT INTO LIVESTOCK (LivestockID, FarmID, AType, LBirthDate, HealthStatus) VALUES (4, 2, 'Pig', DATE '2021-04-30', 'Healthy');
INSERT INTO LIVESTOCK (LivestockID, FarmID, AType, LBirthDate, HealthStatus) VALUES (5, 3, 'Chicken', DATE '2021-05-05', 'Healthy');

-- After inserting data into LIVESTOCK table
SELECT * FROM LIVESTOCK;

-- Before inserting data into EQUIPMENT table
SELECT * FROM EQUIPMENT;

-- Insert records into EQUIPMENT table
INSERT INTO EQUIPMENT (EquipmentID, FarmID, EName, EType, EPurchaseDate, MaintenanceSchedule) VALUES (1, 1, 'Tractor', 'Vehicle', DATE '2022-01-01', 'Quarterly');
INSERT INTO EQUIPMENT (EquipmentID, FarmID, EName, EType, EPurchaseDate, MaintenanceSchedule) VALUES (2, 1, 'Plow', 'Tool', DATE '2022-02-01', 'Yearly');
INSERT INTO EQUIPMENT (EquipmentID, FarmID, EName, EType, EPurchaseDate, MaintenanceSchedule) VALUES (3, 2, 'Harvester', 'Machine', DATE '2022-03-01', 'Monthly');
INSERT INTO EQUIPMENT (EquipmentID, FarmID, EName, EType, EPurchaseDate, MaintenanceSchedule) VALUES (4, 2, 'Sprinkler', 'Irrigation', DATE '2022-04-01', 'Monthly');
INSERT INTO EQUIPMENT (EquipmentID, FarmID, EName, EType, EPurchaseDate, MaintenanceSchedule) VALUES (5, 3, 'Seeder', 'Machine', DATE '2022-05-01', 'Quarterly');

-- After inserting data into EQUIPMENT table
SELECT * FROM EQUIPMENT;

-- Before inserting data into WORKER table
SELECT * FROM WORKER;

-- Insert records into WORKER table
INSERT INTO WORKER (WorkerID, FarmID, FirstName, LastName, Role, ContactInfo) VALUES (1, 1, 'Mike', 'Johnson', 'Farm Manager', 'mike.johnson@gmail.com');
INSERT INTO WORKER (WorkerID, FarmID, FirstName, LastName, Role, ContactInfo) VALUES (2, 1, 'Sarah', 'Williams', 'Field Worker', 'sarah.williams@yahoo.com');
INSERT INTO WORKER (WorkerID, FarmID, FirstName, LastName, Role, ContactInfo) VALUES (3, 2, 'James', 'Jones', 'Livestock Handler', 'james.jones@outlook.com');
INSERT INTO WORKER (WorkerID, FarmID, FirstName, LastName, Role, ContactInfo) VALUES (4, 2, 'Linda', 'Brown', 'Equipment Operator', 'linda.brown@gmail.com');
INSERT INTO WORKER (WorkerID, FarmID, FirstName, LastName, Role, ContactInfo) VALUES (5, 3, 'Tom', 'Davis', 'Farm Manager', 'tom.davis@hotmail.com');

-- After inserting data into WORKER table
SELECT * FROM WORKER;

-- Before inserting data into TASK table
SELECT * FROM TASK;

-- Insert records into TASK table
INSERT INTO TASK (TaskID, FieldID, CropID, LivestockID, Description, WorkerID, TDueDate, Status) VALUES (1, 1, 1, NULL, 'Plant wheat', 2, DATE '2023-03-02', 'Completed');
INSERT INTO TASK (TaskID, FieldID, CropID, LivestockID, Description, WorkerID, TDueDate, Status) VALUES (2, 2, 2, NULL, 'Harvest corn', 2, DATE '2023-08-21', 'Pending');
INSERT INTO TASK (TaskID, FieldID, CropID, LivestockID, Description, WorkerID, TDueDate, Status) VALUES (3, NULL, NULL, 1, 'Check cattle health', 3, DATE '2023-07-10', 'Completed');
INSERT INTO TASK (TaskID, FieldID, CropID, LivestockID, Description, WorkerID, TDueDate, Status) VALUES (4, 3, 3, NULL, 'Plant barley', 4, DATE '2023-05-02', 'Completed');
INSERT INTO TASK (TaskID, FieldID, CropID, LivestockID, Description, WorkerID, TDueDate, Status) VALUES (5, NULL, NULL, 2, 'Shear sheep', 3, DATE '2023-06-01', 'Pending');

-- After inserting data into TASK table
SELECT * FROM TASK;

-- Before inserting data into IRRIGATION_SYSTEM table
SELECT * FROM IRRIGATION_SYSTEM;

-- Insert records into IRRIGATION_SYSTEM table
INSERT INTO IRRIGATION_SYSTEM (IrrigationID, FieldID, IInstallationDate, ICapacity) VALUES (1, 1, DATE '2022-03-01', 100.0);
INSERT INTO IRRIGATION_SYSTEM (IrrigationID, FieldID, IInstallationDate, ICapacity) VALUES (2, 2, DATE '2022-04-01', 200.0);
INSERT INTO IRRIGATION_SYSTEM (IrrigationID, FieldID, IInstallationDate, ICapacity) VALUES (3, 3, DATE '2022-05-01', 150.0);
INSERT INTO IRRIGATION_SYSTEM (IrrigationID, FieldID, IInstallationDate, ICapacity) VALUES (4, 4, DATE '2022-06-01', 180.0);
INSERT INTO IRRIGATION_SYSTEM (IrrigationID, FieldID, IInstallationDate, ICapacity) VALUES (5, 5, DATE '2022-07-01', 220.0);

-- After inserting data into IRRIGATION_SYSTEM table
SELECT * FROM IRRIGATION_SYSTEM;

-- Before inserting data into WEATHER table
SELECT * FROM WEATHER;

-- Insert records into WEATHER table
INSERT INTO WEATHER (WeatherID, FieldID, WDate, Temperature, Rainfall, Humidity) VALUES (1, 1, DATE '2023-07-15', 30.0, 10.0, 60.0);
INSERT INTO WEATHER (WeatherID, FieldID, WDate, Temperature, Rainfall, Humidity) VALUES (2, 2, DATE '2023-08-20', 28.0, 5.0, 55.0);
INSERT INTO WEATHER (WeatherID, FieldID, WDate, Temperature, Rainfall, Humidity) VALUES (3, 3, DATE '2023-09-25', 25.0, 15.0, 70.0);
INSERT INTO WEATHER (WeatherID, FieldID, WDate, Temperature, Rainfall, Humidity) VALUES (4, 4, DATE '2023-10-30', 20.0, 20.0, 80.0);
INSERT INTO WEATHER (WeatherID, FieldID, WDate, Temperature, Rainfall, Humidity) VALUES (5, 5, DATE '2023-11-15', 18.0, 25.0, 75.0);

-- After inserting data into WEATHER table
SELECT * FROM WEATHER;

-- Before inserting data into HARVEST table
SELECT * FROM HARVEST;

-- Insert records into HARVEST table
INSERT INTO HARVEST (HarvestID, CropID, HHarvestDate, Quantity, Quality) VALUES (1, 1, DATE '2023-07-20', 100.0, 'A');
INSERT INTO HARVEST (HarvestID, CropID, HHarvestDate, Quantity, Quality) VALUES (2, 2, DATE '2023-08-25', 150.0, 'B');
INSERT INTO HARVEST (HarvestID, CropID, HHarvestDate, Quantity, Quality) VALUES (3, 3, DATE '2023-09-30', 200.0, 'A');
INSERT INTO HARVEST (HarvestID, CropID, HHarvestDate, Quantity, Quality) VALUES (4, 4, DATE '2023-10-05', 180.0, 'B');
INSERT INTO HARVEST (HarvestID, CropID, HHarvestDate, Quantity, Quality) VALUES (5, 5, DATE '2023-11-20', 220.0, 'A');

-- After inserting data into HARVEST table
SELECT * FROM HARVEST;

-- Before inserting data into BUYER table
SELECT * FROM BUYER;

-- Insert records into BUYER table
INSERT INTO BUYER (BuyerID, BuyerName, ContactInfo) VALUES (1, 'Acme Corp', 'contact@acmecorp.com');
INSERT INTO BUYER (BuyerID, BuyerName, ContactInfo) VALUES (2, 'Farmers Market', 'info@farmersmarket.com');
INSERT INTO BUYER (BuyerID, BuyerName, ContactInfo) VALUES (3, 'Grocery Store', 'sales@grocerystore.com');
INSERT INTO BUYER (BuyerID, BuyerName, ContactInfo) VALUES (4, 'Local Butcher', 'orders@localbutcher.com');
INSERT INTO BUYER (BuyerID, BuyerName, ContactInfo) VALUES (5, 'Organic Foods', 'support@organicfoods.com');

-- After inserting data into BUYER table
SELECT * FROM BUYER;

-- Before inserting data into SALE table
SELECT * FROM SALE;

-- Insert records into SALE table
INSERT INTO SALE (SaleID, HarvestID, BuyerID, SDate, Quantity, Price) VALUES (1, 1, 1, DATE '2023-07-25', 100.0, 500.0);
INSERT INTO SALE (SaleID, HarvestID, BuyerID, SDate, Quantity, Price) VALUES (2, 2, 2, DATE '2023-08-30', 150.0, 750.0);
INSERT INTO SALE (SaleID, HarvestID, BuyerID, SDate, Quantity, Price) VALUES (3, 3, 3, DATE '2023-10-01', 200.0, 1000.0);
INSERT INTO SALE (SaleID, HarvestID, BuyerID, SDate, Quantity, Price) VALUES (4, 4, 4, DATE '2023-10-10', 180.0, 900.0);
INSERT INTO SALE (SaleID, HarvestID, BuyerID, SDate, Quantity, Price) VALUES (5, 5, 5, DATE '2023-11-25', 220.0, 1100.0);

-- After inserting data into SALE table
SELECT * FROM SALE;

-- Before inserting data into STORAGE table
SELECT * FROM STORAGE;

-- Insert records into STORAGE table
INSERT INTO STORAGE (StorageID, FarmID, StorageType, SCapacity, Location) VALUES (1, 1, 'Silo', 500.0, 'Barn 1');
INSERT INTO STORAGE (StorageID, FarmID, StorageType, SCapacity, Location) VALUES (2, 2, 'Warehouse', 1000.0, 'Warehouse 1');
INSERT INTO STORAGE (StorageID, FarmID, StorageType, SCapacity, Location) VALUES (3, 3, 'Cold Storage', 300.0, 'Cold Room 1');
INSERT INTO STORAGE (StorageID, FarmID, StorageType, SCapacity, Location) VALUES (4, 4, 'Shed', 200.0, 'Shed 1');
INSERT INTO STORAGE (StorageID, FarmID, StorageType, SCapacity, Location) VALUES (5, 5, 'Barn', 600.0, 'Barn 2');

-- After inserting data into STORAGE table
SELECT * FROM STORAGE;

-- Before inserting data into INVENTORY table
SELECT * FROM INVENTORY;

-- Insert records into INVENTORY table
INSERT INTO INVENTORY (InventoryID, FarmID, ItemName, Quantity, Unit, ILastUpdated) VALUES (1, 1, 'Seeds', 100.0, 'kg', DATE '2023-07-01');
INSERT INTO INVENTORY (InventoryID, FarmID, ItemName, Quantity, Unit, ILastUpdated) VALUES (2, 2, 'Fertilizer', 200.0, 'kg', DATE '2023-08-01');
INSERT INTO INVENTORY (InventoryID, FarmID, ItemName, Quantity, Unit, ILastUpdated) VALUES (3, 3, 'Pesticides', 150.0, 'L', DATE '2023-09-01');
INSERT INTO INVENTORY (InventoryID, FarmID, ItemName, Quantity, Unit, ILastUpdated) VALUES (4, 4, 'Animal Feed', 300.0, 'kg', DATE '2023-10-01');
INSERT INTO INVENTORY (InventoryID, FarmID, ItemName, Quantity, Unit, ILastUpdated) VALUES (5, 5, 'Machinery Parts', 50.0, 'units', DATE '2023-11-01');

-- After inserting data into INVENTORY table
SELECT * FROM INVENTORY;

-- Before inserting data into VETERINARY table
SELECT * FROM VETERINARY;

-- Insert records into VETERINARY table
INSERT INTO VETERINARY (VetRecordID, LivestockID, VVisitDate, Treatment, Veterinarian) VALUES (1, 1, DATE '2023-07-05', 'Vaccination', 'Dr. Smith');
INSERT INTO VETERINARY (VetRecordID, LivestockID, VVisitDate, Treatment, Veterinarian) VALUES (2, 2, DATE '2023-07-10', 'Check-up', 'Dr. Jones');
INSERT INTO VETERINARY (VetRecordID, LivestockID, VVisitDate, Treatment, Veterinarian) VALUES (3, 3, DATE '2023-07-15', 'Deworming', 'Dr. Brown');
INSERT INTO VETERINARY (VetRecordID, LivestockID, VVisitDate, Treatment, Veterinarian) VALUES (4, 4, DATE '2023-07-20', 'Vaccination', 'Dr. Wilson');
INSERT INTO VETERINARY (VetRecordID, LivestockID, VVisitDate, Treatment, Veterinarian) VALUES (5, 5, DATE '2023-07-25', 'Check-up', 'Dr. Davis');

-- After inserting data into VETERINARY table
SELECT * FROM VETERINARY;

-- Before inserting data into FINANCIAL_RECORD table
SELECT * FROM FINANCIAL_RECORD;

-- Insert records into FINANCIAL_RECORD table
INSERT INTO FINANCIAL_RECORD (FinanceID, FarmID, RecordType, Amount, FDate, Description) VALUES (1, 1, 'Expense', 1000.0, DATE '2023-01-01', 'Seed purchase');
INSERT INTO FINANCIAL_RECORD (FinanceID, FarmID, RecordType, Amount, FDate, Description) VALUES (2, 2, 'Income', 2000.0, DATE '2023-02-01', 'Crop sale');
INSERT INTO FINANCIAL_RECORD (FinanceID, FarmID, RecordType, Amount, FDate, Description) VALUES (3, 3, 'Expense', 1500.0, DATE '2023-03-01', 'Fertilizer purchase');
INSERT INTO FINANCIAL_RECORD (FinanceID, FarmID, RecordType, Amount, FDate, Description) VALUES (4, 4, 'Income', 2500.0, DATE '2023-04-01', 'Livestock sale');
INSERT INTO FINANCIAL_RECORD (FinanceID, FarmID, RecordType, Amount, FDate, Description) VALUES (5, 5, 'Expense', 500.0, DATE '2023-05-01', 'Machinery maintenance');

-- After inserting data into FINANCIAL_RECORD table
SELECT * FROM FINANCIAL_RECORD;

-- Before inserting data into MAINTENANCE_RECORD table
SELECT * FROM MAINTENANCE_RECORD;

-- Insert records into MAINTENANCE_RECORD table
INSERT INTO MAINTENANCE_RECORD (MaintenanceID, EquipmentID, MDate, Description, Cost) VALUES (1, 1, DATE '2023-03-15', 'Oil change', 100.0);
INSERT INTO MAINTENANCE_RECORD (MaintenanceID, EquipmentID, MDate, Description, Cost) VALUES (2, 2, DATE '2023-04-20', 'Blade sharpening', 50.0);
INSERT INTO MAINTENANCE_RECORD (MaintenanceID, EquipmentID, MDate, Description, Cost) VALUES (3, 3, DATE '2023-05-25', 'Belt replacement', 200.0);
INSERT INTO MAINTENANCE_RECORD (MaintenanceID, EquipmentID, MDate, Description, Cost) VALUES (4, 4, DATE '2023-06-30', 'Nozzle cleaning', 75.0);
INSERT INTO MAINTENANCE_RECORD (MaintenanceID, EquipmentID, MDate, Description, Cost) VALUES (5, 5, DATE '2023-07-05', 'Calibration', 150.0);

-- After inserting data into MAINTENANCE_RECORD table
SELECT * FROM MAINTENANCE_RECORD;

-- Before inserting data into TRAINING table
SELECT * FROM TRAINING;

-- Insert records into TRAINING table
INSERT INTO TRAINING (TrainingID, FarmID, Topic, TDate, Trainer) VALUES (1, 1, 'Crop Rotation', DATE '2023-02-10', 'John Expert');
INSERT INTO TRAINING (TrainingID, FarmID, Topic, TDate, Trainer) VALUES (2, 2, 'Pest Management', DATE '2023-03-15', 'Jane Specialist');
INSERT INTO TRAINING (TrainingID, FarmID, Topic, TDate, Trainer) VALUES (3, 3, 'Irrigation Techniques', DATE '2023-04-20', 'Bob Instructor');
INSERT INTO TRAINING (TrainingID, FarmID, Topic, TDate, Trainer) VALUES (4, 4, 'Livestock Care', DATE '2023-05-25', 'Alice Trainer');
INSERT INTO TRAINING (TrainingID, FarmID, Topic, TDate, Trainer) VALUES (5, 5, 'Farm Safety', DATE '2023-06-30', 'Charlie Educator');

-- After inserting data into TRAINING table
SELECT * FROM TRAINING;

-- Before inserting data into COMPLIANCE_RECORD table
SELECT * FROM COMPLIANCE_RECORD;

-- Insert records into COMPLIANCE_RECORD table
INSERT INTO COMPLIANCE_RECORD (ComplianceID, FarmID, Regulation, CInspectionDate, Status) VALUES (1, 1, 'Pesticide Use', DATE '2023-03-01', 'Compliant');
INSERT INTO COMPLIANCE_RECORD (ComplianceID, FarmID, Regulation, CInspectionDate, Status) VALUES (2, 2, 'Animal Welfare', DATE '2023-04-05', 'Compliant');
INSERT INTO COMPLIANCE_RECORD (ComplianceID, FarmID, Regulation, CInspectionDate, Status) VALUES (3, 3, 'Water Usage', DATE '2023-05-10', 'Non-Compliant');
INSERT INTO COMPLIANCE_RECORD (ComplianceID, FarmID, Regulation, CInspectionDate, Status) VALUES (4, 4, 'Organic Certification', DATE '2023-06-15', 'Compliant');
INSERT INTO COMPLIANCE_RECORD (ComplianceID, FarmID, Regulation, CInspectionDate, Status) VALUES (5, 5, 'Worker Safety', DATE '2023-07-20', 'Compliant');

-- After inserting data into COMPLIANCE_RECORD table
SELECT * FROM COMPLIANCE_RECORD;

OPERATIONS


-- 1. Projection on a single column
SELECT FarmName FROM FARM;

-- 2. Selection using a logical operator
SELECT * FROM CROP WHERE CPlantingDate > DATE '2023-04-01';

-- 3. Pattern matching
SELECT * FROM OWNER WHERE FName LIKE 'J%';

-- 4. Join between two tables
SELECT OWNER.FName, OWNER.LName, FARM.FarmName 
FROM OWNER 
JOIN FARM ON OWNER.OwnerID = FARM.OwnerID;

-- 5. Aggregate function (average)
SELECT AVG(FSize) AS Average_Farm_Size FROM FARM;

-- 6. Counting records
SELECT COUNT(*) AS Number_Of_Fields FROM FIELD;

-- 7. Group by and aggregate function
SELECT CROP.CropType, AVG(HARVEST.Quantity) AS Average_Quantity 
FROM HARVEST 
JOIN CROP ON HARVEST.CropID = CROP.CropID 
GROUP BY CROP.CropType;

-- 8. Join and aggregate function
SELECT FARM.FarmName, AVG(HARVEST.Quantity) AS Average_Quantity 
FROM FARM 
JOIN FIELD ON FARM.FarmID = FIELD.FarmID 
JOIN CROP ON FIELD.FieldID = CROP.FieldID 
JOIN HARVEST ON CROP.CropID = HARVEST.CropID
GROUP BY FARM.FarmName;

-- 9. Subquery
SELECT FarmName 
FROM FARM 
WHERE FarmID IN (SELECT FarmID FROM FIELD WHERE FArea > 50);

-- 10. Ordering results
SELECT * FROM LIVESTOCK ORDER BY LBirthDate DESC;

-- 11. Using DISTINCT
SELECT DISTINCT CropType FROM CROP;

-- 12. Using BETWEEN
SELECT * FROM FARM WHERE FSize BETWEEN 100 AND 200;

-- 13. Using IN
SELECT * FROM EQUIPMENT WHERE EType IN ('Vehicle', 'Tool');

-- 14. Join with condition
SELECT FIELD.FieldName, CROP.CropType 
FROM FIELD 
JOIN CROP ON FIELD.FieldID = CROP.FieldID 
WHERE CPlantingDate > DATE '2023-05-01';

-- 15. New Operation: Join and Condition
SELECT OWNER.FName, OWNER.LName, FARM.FarmName, FARM.FSize 
FROM OWNER 
JOIN FARM ON OWNER.OwnerID = FARM.OwnerID 
WHERE FARM.FSize > 150;




UPDATE AND DELETE


-- Display the record before the update
SELECT * FROM FARM WHERE FarmID = 1;

-- Update query
UPDATE FARM SET FSize = 160.0 WHERE FarmID = 1;

-- Display the record after the update
SELECT * FROM FARM WHERE FarmID = 1;

-- Display the records before the delete
SELECT * FROM LIVESTOCK;

-- Delete query
DELETE FROM LIVESTOCK WHERE LivestockID = 5;

-- Display the records after the delete
SELECT * FROM LIVESTOCK;

