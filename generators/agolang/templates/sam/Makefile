.PHONY: build clean deploy gomodgen

build: gomodgen
	export GO111MODULE=on
### yeoman hook ###
## Don't touch this comment, the subgenerator needs it'

access:
	chmod -R u+x ./scripts/

clean:
	rm -rf ./bin ./vendor Gopkg.lock

deploy: access clean build
	./scripts/samdeploy.sh '<%=stackName%>' '$(region)' '$(profile)'

gomodgen:
	chmod u+x gomod.sh
	./gomod.sh

local-api: clean build
	./scripts/samapi.sh '' '$(network)'

api: clean build access
	./scripts/samapi.sh '' '$(network)'

debug-api: clean build access
	./scripts/samapi.sh 'debug' '$(network)'

local-invoke: clean build access
	./scripts/localinvoke.sh '$(func)' '$(event)' '$(network)'

sam-invoke: clean build access
	./scripts/samlocal.sh '$(func)' '$(event)' '$(network)'

debug: clean build access
	./scripts/samdebug.sh '$(func)' '$(event)' '$(network)'

sam-debug: clean build access
	./scripts/samdebug.sh '$(func)' '$(event)' '$(network)'

undeploy: access
	./scripts/samundeploy.sh

test: gomodgen
	go test ./... -cover -count 1