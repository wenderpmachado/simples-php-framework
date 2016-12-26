## Simples framework em PHP ##

### História ###
----------------
Após um bom tempo estudando o [Laravel Framework](https://github.com/laravel/laravel) (PHP) e um pouco de [Rails](https://github.com/rails/rails) (Ruby), de várias pesquisar em relação a quais tecnologias utilizar para projetos em que participo e 
de conversas com amigos de trabalho e faculdade, incluindo professores¹, resolvi reunir o que achava interessante, framework agnóstico e *clean*, junto com algumas ideias vistas no 
Laravel/Rails, com o intuito de utilizar em projetos próprios que não necessitam de grande infraestrutura. 

¹: *Agradecimento especial ao professor [Thiago Delgado Pinto](https://github.com/thiagodp) pelas diversas explicações e ótimas bibliotecas disponibilizadas aqui no github.*

### Arquitetura ###
-------------------
O framework implementa o CRUD baseado no [Repository Pattern](https://github.com/domnikl/DesignPatternsPHP/tree/master/More/Repository).
Cada modelo possui uma pasta com seu nome dentro da pasta principal do projeto, ```app/```, tendo as seguintes classes:

- ModelName
    - Classe referente ao objeto de domínio
    
- ModelNameRepository
    - Interface desse modelo, contendo funções específicas
    - Extende da DefaultRepository, própria do framework, com as funções padrões do CRUD
    
- ModelNameRBRepository
    -   Classe com as regras de negócio referente ao Banco de Dados Relacional
    -   Extende da DefaultRDRepository, própria do framework, com as funções padrões do CRUD já implementadas
    
### Criação das Classes ###
-------------------------------
Para fins de criar essa estrutura, foi criado uma classe chamada ```ClassMaker```, na raiz da pasta ```app```, que deve ser utilizada em um arquivo temporário².
No arquivo temporário seria possível utilizar os métodos:

- makeModel
- makeRepository
- makeController³
    
Exemplo:

```php
require_once __DIR__ . '/vendor/autoload.php';

$classMaker = new ClassMaker();
$className = 'Address';
$parameters = [
    'id' => 'integer',
    'road' => 'string'
];
$classMaker->makeModel($className, $parameters);
$classMaker->makeRepository($className, $parameters);
```
 
²: *Futuramente será implementado a criação dessa estrutura de classes via CLI*
³: *Ainda não implementado*