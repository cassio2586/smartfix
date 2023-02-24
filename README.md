![smartfix](https://user-images.githubusercontent.com/27103177/221184058-f44cdc8d-0805-464c-b85a-b7e8ecae39a7.PNG)

SmartFix é uma distribuição de software livre localizada para o Brasil com fork utilizando o QuickFix/N.

Este README é sobre como configurar seu sistema para o desenvolvimento do SmartFix.

System Setup
------------
Este projeto requer o seguinte:

**Para construir e executar testes**

* [Ruby (2.5+ Recomendado)](http://rubyinstaller.org/) (Usado para gerar mensagens e classes de campo do arquivo xml DataDictionary)
* Na linha de comando: dotnet 2.0.0 or maior
* No Visual Studio: versão 2017 or maior

Geração de código
---------------
Para regenerar a mensagem e a origem da classe de campo dos dicionários de dados,
você precisa do Ruby e da gema Nokogiri:

```
gem install nokogiri
ruby generator\generate.rb
```

Build
-----
Para construir o projeto, execute:

```
build.bat
```

You can also override the default configuration (Release) by giving a command line argument:

```
build.bat Debug
```


O script build.bat espera que dotnet esteja no PATH.

Como alternativa, basta usar as ferramentas dotnet.

Testes unitários
----------
Para executar os testes NUnit, execute:

```
unit_test.bat
```

(Este script espera que `dotnet` esteja no PATH.)

Os relatórios TRX dos resultados do teste (um para NET Framework 4.5.2 e NET Standard 2.0) estarão disponíveis aqui:

```
UnitTests\TestResults
```

Alternativamente, simplesmente use `dotnet`:

```
dotnet test UnitTests
```

Para executar testes unitários no depurador:

1. Abra o TestExplorer em Test -> Windows -> Test Explorer
2. Navegue até o teste
3. Clique com o botão direito do mouse e selecione "Depurar testes selecionados"


Testes de aceitação
----------------
Para executar o conjunto completo de testes de aceitação:

```
acceptance_test.ps1
```

Um relatório HTML dos resultados do teste estará disponível aqui:

    AcceptanceTests\AcceptanceTests.html

Para executar um teste de aceitação específico, e.g. fix42\14e_IncorrectEnumValue.def:

```
cd AcceptanceTest
pwsh runat.ps1 release 5003 definitions\server\fix42\14e_IncorrectEnumValue.def cfg\at_42.cfg net6.0
```
O parâmetro final *deve* ser "net6.0".

(Consulte accept_test.ps1 para obter os números de porta e arquivos de configuração apropriados para usar no comando acima.)

Os resultados do teste estarão disponíveis em AcceptanceTests\TestResults.xml e
as informações de depuração estarão disponíveis no diretório AcceptanceTests\log.

Para executar um teste no depurador,

  1. Abra o arquivo de solução no Visual Studio
  2. Clique com o botão direito do mouse no projeto "AcceptanceTest" e escolha "Propriedades" no menu
  3. Clique em "Depurar" na barra de navegação à esquerda
  4. Defina "Argumentos de linha de comando" para o "cfg\at_XX.cfg" relevante para seu teste
  5. Defina o diretório de trabalho como "[yourpath]\quickfixn\AcceptanceTest"
  6. Salve as propriedades
  7. Clique com o botão direito do mouse no projeto "AcceptanceTest", vá para Debug -> Start New Instance
  8. No terminal de comando, vá para o diretório "AcceptanceTest"
  9. Execute: `ruby Runner.rb 127.0.0.1 5001 settings\server\fix42\YourTestName.def`

Credits
-------

Cassio Antunes - Engenheiro de Software

Licenciamento
---------

Este software está disponível sob a Licença de Software QuickFIX. Consulte a [LICENÇA](LICENÇA) para os termos especificados pela Licença de Software QuickFIX.

[1]: http://quickfixn.org/web/public/images/qfn-logo/QuickFIX-n_logo-small.png
