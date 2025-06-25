## Create vs Build
### Create
`FactoryBot.create(:account)` will create an account object and all associatioins for it, and they will all be peersisted in the database. It will also trigger model and database validations.

### Build
`FactoryBot.build(:account)` will make requests to a database id the factory has associations but it won't save the object. It will trigger validations only for associated objects.
