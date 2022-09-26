![Oicina Mecanica](https://user-images.githubusercontent.com/31481414/188243373-74c69ae7-1724-4ba9-a45d-bb00be060795.png)
# Oficina_Mecanica


create database oficina;
use oficina;

create table cliente(
idCliente int primary key,
Nome varchar(45),
Endereço varchar (45),
Forma_de_pagamento varchar(45)
);
drop table veículo;
create table veículo(
idVeiculo int primary key,
placa char (7),
marca varchar(45),
modelo varchar (45),
idCliente int,
constraint fk_idCliente foreign key (idCliente) references cliente(idCliente)

);

create table pedido_avaliação (
idPedido int primary key,
avaliação_veiculo varchar (100),
data_solicitação date,
idCliente int ,
idVeiculo int ,
constraint fk_idclienteped foreign key  (idCliente) references cliente(idCliente),
constraint fk_id_veiculo foreign key  (idVeiculo) references veículo(idVeiculo)
);

create table equipeMeanico(
idEquipeMecanico int primary key,
NomeMecanico  varchar (200),
MEndereço varchar (200),
Especialidade varchar (100)
 
);
desc tipo_serviço;
alter table tipo_serviço add  column idVeículo int;
create table tipo_Serviço (
idTipoServiço int primary key,
Tipo_de_Serviço enum('revisão','conserto')

);
alter table Os add  column idVeículo int;
select*from Os;
create table Os(
idOs int primary key,
data_emissao date,
valor float,
StatusServiço varchar(45),
data_conclusao date

);

create table conserto (
idConserto int primary key,
Tipo_de_conserto varchar(45),
idTipoServiço  int,
idOs int,
CValor_mao_de_obra float,
constraint fk_tiposerviço foreign key  (idTipoServiço) references Tipo_Serviço(idTipoServiço ),
constraint fk_idOscon foreign key  (idOs) references Os(idOs)

);
create table maodeobra(
idMao_de_obra int primary key,
Mvalor float

);
create table peça(
idpeça int primary key,
Pnome varchar (45),
Pvalor float

);
create table pecaConserto(
idpeça int primary key,
idConserto int,
idTipoServiço int,
constraint fk_idpecaC foreign key  (idpeça) references peça(idpeça),
constraint fk_idconserto foreign key  (idConserto) references conserto(idConserto),
constraint fk_tiposerviçoP foreign key  (idTipoServiço) references Tipo_Serviço(idTipoServiço)
);
alter table revisao add  column idTipoServiço int;
create table revisao(
idRevisao int primary key,
PeriodoRevisão enum ('anual','mensal','km'),
RValor_mao_de_obra float,
idOs int,
constraint fk_idOsRev foreign key  (idOs) references Os(idOs)
);
create table autorizaçaoServiço(
idCliente int,
idOs int,
Status_Autorização varchar (20),
constraint fk_idOsAut foreign key  (idOs) references Os(idOs),
constraint fk_idclienteAut foreign key  (idCliente) references Cliente(idCliente)
);
create table execução_serviço(
idCliente int,
idOs int,
idEquipeMecanico int,
idTipoServiço int,
previsao_entrega date,
constraint fk_idOsExec foreign key  (idOs) references Os(idOs),
constraint fk_idclienteExec foreign key  (idCliente) references Cliente(idCliente),
constraint fk_idequipeMecanicoExec foreign key  (idEquipeMecanico) references EquipeMeanico(idEquipeMecanico),
constraint fk_idtiposervicoExec foreign key  (idTipoServiço) references Tipo_Serviço(idTipoServiço)


);
show tables;
desc cliente;
insert into cliente values (1,'joao','rua dos anzois', 'cartao'),
(2,'andre','rua dos caracois', 'dnheiro'),
(3,'thayana','rua dos gatos', 'cartao');

desc veículo;
select*from veículo;
insert into veículo values(1,'abm6j44','volks','voyage',1),
(2,'abm6j45','volks','kombi',2),
(3,'abm6j54','volks','gol',3);

desc tipo_serviço;
select*from pedido_avaliação;
insert into pedido_avaliação values(1, 'inicial', '2022-05-12', 1,1),
(2, 'inicial', '2022-06-14', 2,2),
(3, 'inicial', '2022-06-12', 3,3);
select*from Tipo_serviço;
insert into Tipo_Serviço values(11,'revisão',1),
(22,'revisão',2),
(33,'conserto',3);

show tables;
desc revisao;
select *from revisao;
insert into revisao values(1,'anual',50,1,11),
(2,'mensal',55,2,22);

desc Os;
select *from Os;
insert into Os values(1,'2022-10-12',100,'em avaliação', '2022-11-10',1),
(2,'2022-10-12',100,'em avaliação', '2022-12-10',2),
(3,'2022-10-12',100,'em avaliação', '2022-11-11',3);

select Nome n, marca m
from  cliente n join veículo m;
