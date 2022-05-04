
Crição do arquivo app.yml, parâmetros para consulta ao webservice DO CATI no Portal de Gestão.

Solicitamos a criação do arquivo app.yml no Portal Integrado de Gestão, para armazenar o endereço e as credenciais de acesso ao webservice do sistema CATI. Segue a contextualização.

O módulo “Gestão de chamados da DTI” realiza consultas ao sistema do CATI através de duas telas durante o ciclo de gerenciamento de um chamado:

1 – No cadastro de um novo chamado:

![image](https://user-images.githubusercontent.com/15015013/166695313-7f6bc595-68aa-46e3-a658-a6118c75fffa.png)

2 – Na opção “Adicionar referência” em um chamado já cadastrado:

![image](https://user-images.githubusercontent.com/15015013/166695657-37501e14-9da6-4c32-bfe1-a727cb25937b.png)

Em versões anteriores do Portal de Gestão, a integração da consulta ao CATI era realizada por meio de uma consulta direta ao banco de dados. Após a atualização do sistema CATI a consulta ficou indisponível, pois a versão do PHP do Portal de Gestão (5.3) é incompatível com a versão do banco de dados MySQL do CATI.

Para contornar esse problema com o mínimo de intervenção possível, e devido a criticidade dos sistemas envolvidos, verificamos que o sistema OTRS (CATI), disponibiliza “endpoints” para consultas aos chamados. A opção de webservice se mostrou viável e mais adequada do que consultas diretas ao banco.

Na implementação da consulta ao webservice há a necessidade de armazenar as credenciais de acesso, em projetos symfony 1.4, por padrão, esse tipo de informação é armazenado no arquivo app.yml, no mesmo nível do arquivo que armazena as credenciais de acesso ao banco de dados (\config\app.yml). 
Este arquivo não pode sofrer alterações durante o processo de deploy, e cada ambiente (DEV, HOM, PROD) utiliza as respectivas credenciais.

O arquivo app.yml tem a seguinte estrutura, exemplo do ambiente de homologação:


	all:

  		webservice:
	
			url: https://cati.hom.capes.gov.br/otrs/nph-genericinterface.pl/Webservice/portal_gestao
	
			username: loremipsum
		
			password: loremipsum

Para a disponibilizarmos a nova consulta em produção o arquivo deve ser criado conforme o exemplo acima.
