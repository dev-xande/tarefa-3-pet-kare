## Rota de criação

- Caso o usuário tente inserir um dado de pet com grupo ou características que já estão salvas no banco de dados, não deve ser criado novamente o grupo ou a(s) característica(s) e sim devem ser utilizados os registros que já existem. Então, por exemplo, caso haja a característica "clever" atribuída ao pet "Seraphim" e o usuário tentar criar outro pet com esse mesmo atributo, a sua aplicação deve pegar a característica "clever" que já existe no banco e associar ao novo pet, evitando assim repetições desnecessárias no banco de dados. A mesma tratativa deve ser feita em relação a grupos.
- Ao inserir um sex inválido conforme seus choices deve ser retornado um erro conforme o exemplo

## Rota de atualização

- Todos os campos na requisição devem ser opcionais e todos os dados do pet podem ser modificados.
- Caso seja passado o campo group ou o campo traits, ambos devem seguir a mesma regra de negócio mencionada no create, ou seja, se o grupo ou características já existirem no banco, você deverá pegar as que já existem invés de criar novas.
- No caso do campo group ser passado para atualização, simplesmente deve ser reassociado o novo grupo ao pet, desfazendo o relacionamento anterior.
- Quanto ao campo traits, se ele for passado para atualização, as novas características deverão substituir todas as características anteriores do pet, ou seja, qualquer relacionamento anterior do pet com as características devem ser desfeitos, dando lugar as novas características atualizadas.


...

Body JSON
```python
{
  "name": "Seraphim",
  "age": 1,
  "weight": 20,
  "sex": "Tralala",
  "group": {"scientific_name": "canis familiaris"},
  "traits": [{"name": "clever"}, {"name": "friendly"}]
}
```
Retorno JSON - Status 400 BAD REQUEST
```python
{
	"sex": [
		"\"Tralala\" is not a valid choice."
	]
}
```
