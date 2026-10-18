.PHONY: build server deploy release clean

build:
	hugo --gc --minify

server:
	hugo server --buildDrafts

deploy:
	@test -n "$(deploy_user)" -a -n "$(deploy_server)" || { echo "set deploy_user and deploy_server"; exit 1; }
	rsync -avz public/ $(deploy_user)@$(deploy_server):/home/$(deploy_user)/www/huesler.io/

release: clean build deploy

clean:
	rm -rf public resources
