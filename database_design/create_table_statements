drop table if exists fills;
drop table if exists prescription;
drop table if exists patient;
drop table if exists pharma_drug_price;
drop table if exists drug;
drop table if exists contract;
drop table if exists supervisor;
drop table if exists retail_pharma;
drop table if exists pharma_company;
drop table if exists doctor;

create table retail_pharma(
    pharmacy_id varchar(10),
    name varchar(30),
    address varchar(50),
    phone_number varchar(12),
    primary key (pharmacy_id)
);

create table pharma_company(
    company_id varchar(10),
    name varchar(30),
    primary key (company_id)
);

create table doctor(
    SSN varchar(11),
    name varchar(30) not null,
    specialty varchar(20),
    primary key (SSN)
);

create table supervisor(
    id varchar(10),
    email varchar(40),
    phone_number varchar(12),
    address varchar(50),
    primary key (id)
);

create table patient(
    SSN varchar(11),
    name varchar(30) not null,
    birth_date varchar(10),
    address varchar(50),
    age numeric (3,0),
    d_SSN varchar(11),
    pharmacy_id varchar(10),
    primary key(SSN),
    constraint patient1 foreign key (d_SSN) references doctor(SSN)
        on delete set null, 
    constraint patient2 foreign key (pharmacy_id) references retail_pharma(pharmacy_id)
        on delete set null
);

create table drug(
    drug_id varchar(10),
    generic_name varchar(30),
    trade_name varchar(30) unique,
    company_id varchar(10),
    primary key (drug_id),
    constraint drug1 foreign key (company_id) references pharma_company(company_id)
);

create table prescription(
    rxid varchar(10),
    date_prescribed varchar(10),
    quantity tinyint,
    refill_allowed boolean,
    drug_id varchar(10),
    d_SSN varchar(11),
    p_SSN varchar(11),
    primary key (rxid),
    constraint prescription1 foreign key (d_SSN) references doctor(SSN)
        on delete cascade,
    constraint prescription2 foreign key (p_SSN) references patient(SSN)
        on delete cascade,
    constraint prescription3 foreign key (drug_id) references drug(drug_id)
        on delete cascade
);

create table fills(
    fill_no varchar(10),
    date_filled varchar(10),
    rxid varchar(10),
    pharmacy_id varchar(10),
    company_id varchar(10),
    primary key(fill_no),
    constraint fills1 foreign key (rxid) references prescription(rxid)
        on delete cascade,
    constraint fills2 foreign key (pharmacy_id) references retail_pharma(pharmacy_id),
    constraint fills3 foreign key (company_id) references pharma_company(company_id)
);

create table pharma_drug_price(
    price numeric(6,2),
    pharmacy_id varchar(10),
    drug_id varchar(10),
    primary key (pharmacy_id, drug_id),
    constraint pharma_drug_price1 foreign key (pharmacy_id) references retail_pharma(pharmacy_id)
        on delete cascade,
    constraint pharma_drug_price2 foreign key (drug_id) references drug(drug_id)
        on delete cascade
);

create table contract(
    contract_id varchar(10),
    s_id varchar(10),
    pharmacy_id varchar(10),
    company_id varchar(10),
    primary key (contract_id),
    constraint contract1 foreign key (s_id) references supervisor(id),
    constraint contract2 foreign key (pharmacy_id) references retail_pharma(pharmacy_id)
        on delete cascade,
    constraint contract3 foreign key (company_id) references pharma_company(company_id)
        on delete cascade
);
