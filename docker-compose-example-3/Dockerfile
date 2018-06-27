FROM alpine
LABEL "maintainer" = "andrewnascimento <afn3286@gmail.com>"
RUN apk update && apk add ruby
RUN gem update --system
RUN gem install rubygem-json --no-ri --no-rdoc
RUN gem install sinatra --no-ri --no-rdoc
RUN gem install redis --no-ri --no-rdoc
ADD counter.rb counter.rb
ADD Gemfile Gemfile
EXPOSE 4567
ENTRYPOINT ["ruby","counter.rb"]