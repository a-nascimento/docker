FROM ruby
EXPOSE 4567
ENTRYPOINT ["bundle","exec","rackup","-p,"4567","--host","0.0.0.0"]
ONBUILD AD . /
ONBUILD RUN bundle install
