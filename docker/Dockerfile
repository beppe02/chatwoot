FROM ruby:3.1-slim

ENV RAILS_ENV=production \
    NODE_ENV=production \
    BUNDLE_WITHOUT="development test"

RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    nodejs \
    yarn \
    postgresql-client \
    git \
    libvips \
    imagemagick \
    && apt-get clean

# 🔧 CREA la directory prima di usarla
RUN mkdir -p /app
WORKDIR /app

COPY . .

# ✅ CREA il file evitando l'errore
RUN echo "render-deploy" > /app/.git_sha

RUN bundle install
RUN yarn install
RUN bundle exec rails assets:precompile

EXPOSE 3000

CMD ["bundle", "exec", "rails", "s", "-b", "0.0.0.0"]
