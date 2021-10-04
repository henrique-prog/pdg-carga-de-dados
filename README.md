# Sugestão para Carga de dados do Programa de Gestão!

O processo de carga do sistema do programa de gestão- SISGP ainda não está automatizado, portanto é necessária a extração dos dados do Sistema Integrado de Administração de Recursos Humanos (Siape) para subsidiá-lo. Como boa prática, para melhor execução do SISGP e funcionamento do programa, sugerimos que sejam seguidas as recomendações abaixo para extração dos dados do SIAPE: 

O processo de extração do SIAPE e carga do SISGP deve ocorrer com a maior frequência possível para que as informações estejam sempre atualizadas. Consideramos razoável que o processo de extração/carga seja realizado semanalmente. 

Os perfis de chefia e servidor são atribuídos pelo SISGP com base nas informações extraídas do SIAPE, por isso é importante que esses dados reflitam a realidade de trabalho do participante, assim suas chefias terão condições de pactuar planos de trabalho, fazer avaliação das entregas e até autorizar suas férias. Assim, sugerimos a extração dos dados com base na UORG de emissão dos agentes públicos, pois esta contemplará, além dos servidores efetivos, os servidores sem vínculo e temporários e suas unidades de efetiva atuação. 

Caso não seja possível a extração com base na UORG de emissão, deverão ser usadas, preferencialmente nesta ordem, as UORGs de exercício, de localização e, por fim, de lotação. Importante ressaltar que, para o SISGP, todas essas informações são denominadas “unidade de lotação”. 

Caso seja necessário alterar a lotação e/ou exercício do servidor para adequação à realidade do programa de gestão, orienta-se que seja feito ato administrativo próprio para este fim, a critério do órgão/entidade. 

Excepcionalmente, em situações em que não seja possível a adequação sugerida anteriormente, recomendamos que a chefia que acompanha a execução das atividades do participante, reporte formalmente à chefia prevista no sistema do programa de gestão as informações necessárias para que este possa efetivar os devidos registros.

Descreve-se abaixo sugestões para procedimentos no processo de carga e manutenção de dados no Sistema de Programa de Gestão, aqui chamado SISPG, ferramenta de apoio tecnológico para acompanhamento e controle do cumprimento de metas e alcance de resultados nos termos da Instrução Normativa Nº 65, de 30 de julho de 2020. Esse é um documento técnico destinado às áreas de tecnologia dos órgãos que adotaram o SISPG como ferramenta de gestão do teletrabalho. 

> **Importante:** Este manual não tem caráter exaustivo, sendo portanto, ferramenta de apoio à compreensão dos procedimentos a serem adotados para a carga do banco de dados.

A carga de dados se dá a partir do sistema de recursos humanos do órgão para a base do SISPG pela extração dos dados do SIAPE. As tabelas que devem ser populadas são: **Unidade, Pessoa e Função**.

Os campos **"tipoUnidadeId" e "tipoFuncaoUnidadeId" da tabela "Unidade"** não relacionam-se com o PGD. Essa aplicação, na SUSEP faz parte de um sistema maior, que integra RH, etc. Durante o saneamento das tabelas para o PGD ficaram esses campos. Podem desconsiderá-los, preenchendo null por exemplo.

### Fluxo proposto:

> **Dep RH -->>** Faz a extração SIAPE e transformação <br/>dos dados para a planilha, conforme MODELO
>**Dep TI-->>** Carrega na base do SISPG a partir do ETL Pentaho

>>**Nota:**  No Ministério da Economia o processo foi alinhado com a DGP, que extrai os dados do SIAPE e montagem da planilha de carga.

## Passo a passo para utilização da solução


> **1.**  Baixar todos os arquivos.

> **2.** Petanho precisa estar configurado e instalado com a biblioteca JTDS instalada em **C:\data-integration\lib** (copiar o arquivo .JAR aqui). Disponível para download em:  https://sourceforge.net/projects/jtds/

> **3.** Abrir o arquivo PROG_GESTAO_JOB_UNICO no pentaho.

> **4.**  Abrir o step "Set variables" e configurar as seguintes variáveis:
>>**4.1.** CAMINHO_DO_ARQUIVO: valor deve apontar para o .xlsx
>>**4.2.** DB_host: endereço IP do servidor do banco de dados
>>**4.3.** DB_user: usuário do banco de dados
>>**4.4.** DB_senha: senha desse usuário
>>**4.5.** DB_porta: porta de rede 
>>**4.6.** DB_nome: nome do banco

>**5.** Rodar o JOB localmente. (Run, ou apertar F9)
