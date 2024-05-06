# ponderada3_RDS

Para atender aos requisitos solicitados, vamos seguir as etapas abaixo:

# 1. Modelo Lógico e Diagrama do Banco de Dados
Primeiro, vamos criar um modelo lógico simples para o problema proposto. Considerando que estamos lidando com um sistema de transporte de pacientes, podemos ter entidades como Veículo, Paciente, Transporte, e Registro de Transporte.

Modelo Lógico:
'''
Table Paciente {
  paciente_id int [pk]
  nome varchar(100)
  data_nascimento date
  endereco varchar(255)
  numero_contato varchar(20)
  historico_medico longtext
}

Table UnidadeSaude {
  unidade_id int [pk]
  nome varchar(100)
  tipo varchar(50)
  endereco varchar(255)
  capacidade_atendimento int
}

Table ProdutoMedico {
  produto_id int [pk]
  nome varchar(100)
  tipo varchar(50)
  descricao longtext
  quantidade_estoque int
}

Table VeiculoTransporte {
  veiculo_id int [pk]
  tipo varchar(50)
  capacidade int
  disponibilidade boolean
}

Table RotaTransporte {
  rota_id int [pk]
  origem varchar(255)
  destino varchar(255)
  distancia_km decimal(10, 2)
  tempo_viagem_minutos int
  veiculo_id int [ref: > VeiculoTransporte.veiculo_id]
}

Table TransportePaciente {
  transporte_id int [pk]
  paciente_id int [ref: > Paciente.paciente_id]
  rota_id int [ref: > RotaTransporte.rota_id]
  data_transporte varchar(255)
}
'''

# Modelo Lógico - Imagem
![alt text](images/modelologico.png)

# Relações Cardinais das tabelas
Nesse tópico, eu fiz relações de possíveis tabelas também. Pois, no enunciado da ponderada, é solicitado um modelo mínimo que responda a questão. Entretanto, percebi outras tabelas que poderiam ser elaboradas.

Relação 1:N entre Paciente e TransportePaciente:
Um paciente pode ter múltiplos registros de transporte (por exemplo, visitas médicas ou transferências entre unidades de saúde).
Cada registro de transporte está associado a um único paciente.

Relação N:1 entre UnidadeSaude e TransportePaciente:
Muitos registros de transporte estão associados a uma única unidade de saúde (por exemplo, transportes que vão para uma clínica específica).
Cada registro de transporte é direcionado para uma única unidade de saúde.

Relação N:1 entre RotaTransporte e TransportePaciente:
Muitos registros de transporte estão associados a uma única rota de transporte específica.
Cada registro de transporte é realizado conforme uma rota específica.

Relação N:1 entre RotaTransporte e VeiculoTransporte:
Muitas rotas de transporte são realizadas por um único veículo.
Cada rota de transporte é atribuída a um veículo específico.

Relação 1:N entre ProdutoMedico e UnidadeSaude:
Cada unidade de saúde pode receber múltiplos produtos médicos (medicamentos, equipamentos, suprimentos).
Cada produto médico está associado a uma única unidade de saúde.

Relação N:N entre ProdutoMedico e TransportePaciente (não explicitamente modelada nas tabelas fornecidas, mas implícita no cenário descrito):
Um transporte de paciente pode envolver a entrega de produtos médicos específicos (por exemplo, medicamentos).
Um produto médico pode ser transportado em vários registros de transporte de paciente para diferentes unidades de saúde.

# Deploy no MySQL RDS da AWS
Acesse o Console AWS e vá para o serviço RDS.
Crie uma nova instância de banco de dados MySQL.
Configure os detalhes da instância (tipo de instância, capacidade, nome do banco de dados, etc.).
Garanta que a instância RDS tenha acesso adequado (por exemplo, ajuste grupos de segurança para permitir acesso a partir do local desejado).
Após a criação, conecte-se ao banco de dados usando um cliente MySQL (por exemplo, MySQL Workbench) e crie as tabelas com base no modelo lógico.

# Fluxo da ponderada
- Primeiro criei uma instância RDS na AWS
- Fiz o deploy do MySQL nessa RDS
- Desenhei um modelo lógico no papel
- Passei para o dbdiagram.io
- Adaptei as entidades e relacionamentos propostas acima ao diagrama
- Acessei meu banco de dados pelo MySQL Workbench
- Criei as tabelas com base nos modelos que eu desenhei
- Insiri todos os dados necessários nas tabelas para consultas
- Fiz a consulta

# Fluxo da ponderada - Imagens
![alt text](images/imaga1.jpg)
![alt text](images/imagee3.jpg)
![alt text](images/image2.jpg)
![alt text](images/image4.jpg)
![alt text](images/image5.jpg)

# Resultado consulta final
![alt text](images/image6.jpg)
