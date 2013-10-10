## 1 - Tutorial para usar o geplanes no JBoss 7.1.1

No manual de instalação/atualização é descrito em maiores detalhes a instalação e configuração do geplanes:

[http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/Manual_de_Atualiza%C3%A7%C3%A3o_para_a_Vers%C3%A3o_3.0.3.pdf](http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/Manual_de_Atualiza%C3%A7%C3%A3o_para_a_Vers%C3%A3o_3.0.3.pdf)

## 2 - Aqui mostraremos apenas o que configurar no JBoss 7 para que o geplanes funcione adequadamente

<b>Observações:</b>

* O arquivo build <b>geplanes_bsc.war</b> é o mesmo, apenas serão alterados alguns arquivos de configuração do próprio JBoss.

* Não é necessário alterar a configuração de memória de inicialização do jboss uma vez que por padrão ele já incializa com 2GB de ram.

* O arquivo <b>jboss7+geplanes3.0.3.tar</b> já vem com o jboss configurado e com o geplanes junto.

## 2.1 - Editar o arquivo applicationConfig.xml

Editar o arquivo <i>applicationConfig.xml</i> em (<i>path/jboss-7.1.1.Final/standalone/deployments/geplanes_bsc.war/WEB-INF</i>)

Adicione o seguinte trecho logo após o bean <i>"authenticationConfig"</i>:

    <bean id="dataSource"
        class="br.com.linkcom.sgm.util.JndiGeplanesFactory">
    </bean>

## 2.2 - Editar o arquivo standalone.xml

Editar o arquivo <i>standalone.xml</i> em (<i>path/jboss-7.1.1.Final/standalone/configuration</i>)

Adicione os trechos dentro da tag <i><datasources></i>. Essa configuração substitui a configuração do banco de dados definida no arquivo <i>geplanes_bsc_geplanes-ds.xml</i> utilizada para a versÃ£o 4.5 do JBoss.

No exemplo abaixo o ip do servidor do banco de dados é o 10.0.1.6.

    <datasources>
        <datasource jta="false" jndi-name="java:/10.0.1.6_geplanes_bsc_PostgreSQLDS" pool-name="postgresDS05" enabled="true" use-java-context="true" use-ccm="false">
          <connection-url>jdbc:postgresql://localhost:5432/geplanes_bsc</connection-url>
          <driver-class>org.postgresql.Driver</driver-class>
          <driver>postgresql</driver>
          <pool>
            <min-pool-size>2</min-pool-size>
            <max-pool-size>20</max-pool-size>
          </pool>
          <security>
            <user-name>postgres</user-name>
            <password>postgres</password>
          </security>
          <validation>
            <validate-on-match>false</validate-on-match>
            <background-validation>false</background-validation>
            <background-validation-millis>1</background-validation-millis>
          </validation>
          <statement>
            <prepared-statement-cache-size>0</prepared-statement-cache-size>
            <share-prepared-statements>false</share-prepared-statements>
          </statement>
        </datasource>
        <datasource jta="false" jndi-name="java:/geplanes_bsc_PostgreSQLDS" pool-name="postgresDS01" enabled="true" use-java-context="true" use-ccm="false">
          <connection-url>jdbc:postgresql://localhost:5432/geplanes_bsc</connection-url>
            <driver-class>org.postgresql.Driver</driver-class>
            <driver>postgresql</driver>
            <pool>
              <min-pool-size>2</min-pool-size>
              <max-pool-size>20</max-pool-size>
            </pool>
            <security>
              <user-name>postgres</user-name>
              <password>postgres</password>
            </security>
            <validation>
              <validate-on-match>false</validate-on-match>
              <background-validation>false</background-validation>
              <background-validation-millis>1</background-validation-millis>
            </validation>
            <statement>
              <prepared-statement-cache-size>0</prepared-statement-cache-size>
              <share-prepared-statements>false</share-prepared-statements>
            </statement>
        </datasource>
        <datasource jta="false" jndi-name="java:/127.0.0.1_geplanes_bsc_PostgreSQLDS" pool-name="postgresDS02" enabled="true" use-java-context="true" use-ccm="false">
          <connection-url>jdbc:postgresql://localhost:5432/geplanes_bsc</connection-url>
          <driver-class>org.postgresql.Driver</driver-class>
          <driver>postgresql</driver>
          <pool>
            <min-pool-size>2</min-pool-size>
            <max-pool-size>20</max-pool-size>
          </pool>
          <security>
            <user-name>postgres</user-name>
            <password>postgres</password>
          </security>
          <validation>
            <validate-on-match>false</validate-on-match>
            <background-validation>false</background-validation>
            <background-validation-millis>1</background-validation-millis>
          </validation>
          <statement>
            <prepared-statement-cache-size>0</prepared-statement-cache-size>
            <share-prepared-statements>false</share-prepared-statements>
          </statement>
        </datasource>
        <datasource jta="false" jndi-name="java:/localhost_geplanes_bsc_PostgreSQLDS" pool-name="postgresDS" enabled="true" use-java-context="true" use-ccm="false">
          <connection-url>jdbc:postgresql://localhost:5432/geplanes_bsc</connection-url>
          <driver-class>org.postgresql.Driver</driver-class>
          <driver>postgresql</driver>
          <pool>
            <min-pool-size>2</min-pool-size>
            <max-pool-size>20</max-pool-size>
          </pool>
          <security>
            <user-name>postgres</user-name>
            <password>postgres</password>
          </security>
          <validation>
            <validate-on-match>false</validate-on-match>
            <background-validation>false</background-validation>
            <background-validation-millis>1</background-validation-millis>
          </validation>
          <statement>
            <prepared-statement-cache-size>0</prepared-statement-cache-size>
            <share-prepared-statements>false</share-prepared-statements>
          </statement>
        </datasource>
        <datasource jndi-name="java:jboss/datasources/ExampleDS" pool-name="ExampleDS" enabled="true" use-java-context="true">
            <connection-url>jdbc:h2:mem:test;DB_CLOSE_DELAY=-1</connection-url>
            <driver>h2</driver>
            <security>
              <user-name>sa</user-name>
              <password>sa</password>
            </security>
        </datasource>
            <drivers>
              <driver name="h2" module="com.h2database.h2">
                <xa-datasource-class>org.h2.jdbcx.JdbcDataSource</xa-datasource-class>
              </driver>
              <driver name="postgresql" module="org.postgresql">
                <xa-datasource-class>org.postgresql.xa.PGXADataSource</xa-datasource-class>
              </driver>
            </drivers>
      </datasources>

## 2.3 - Criar o arquivo geplanes_bsc.war.dodeploy

Criar o arquivo <b>geplanes_bsc.war.dodeploy</b> no caminho <i>path/jboss-7.1.1.Final/standalone/deployments</i> com o seguinte conteúdo:
   
    geplanes_bsc.war

## 2.4 - Copiar o driver do postgresql postgresql-9.2-1002.jdbc4.jar

Copiar o driver do postgresql (<i>postgresql-9.2-1002.jdbc4.jar</i>) dentro da pasta <i>path/jboss-7.1.1.Final/modules/org/postgresql/main</i>

## 2.5 - Criar um script para facilitar a inicialização do jBoss.

Criar o arquivo com o nome jboss7 na pasta <i>/etc/init.d</i>
 
     # sudo nano /etc/init.d/jboss7

Colar o conteúdo:
  
     #!/bin/bash
     #Define JBOSS_HOME
     JBOSS_HOME=/path/jboss-7.1.1.Final

     case "$1" in
     start)
     echo "Subindo JBoss AS7..."
     sh ${JBOSS_HOME}/bin/standalone.sh & > /dev/null

     ;;
     stop)
     echo "parando JBoss AS7..."
     sh ${JBOSS_HOME}/bin/jboss-cli.sh --connect command=:shutdown
     ;;
     log)
     echo "log server.log..."
      tail -1000f ${JBOSS_HOME}/standalone/log/server.log
     ;;
     *)
     echo "Use: /etc/init.d/jboss7 {start|stop|log}"
     exit 1
     ;; esac
     exit 0


E agorar dar permissÃ£o de execução ao arquivo:

    # sudo chmod +x /etc/init.d/jboss7

Para iniciar o serviço:

    # sudo /etc/init.d/jboss7 start

E para parar o serviço:

    # sudo /etc/init.d/jboss7 stop

}
