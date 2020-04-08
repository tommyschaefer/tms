---
layout: post
title: Routing Slack API Events in Rails
link: https://labs.teecom.com/2020/04/07/routing-slack-api-events-in-rails.html
originally_posted_on: TEECOMlabs blog
---

On a recent Rails project I needed to handle incoming events from the Slack API.
All Slack event notifications are sent to a single URL, so I wasn't sure how
best to structure this inside of a Rails application. In the past, I've used a
single controller to handle events, but that never quite sat right with me. I
wanted to try something different this time.

After reading up on request-based routing constraints in the
[Rails documentation](https://guides.rubyonrails.org/routing.html),
I decided to experiment with them. I really wanted to route `URL Verification`
and `Link Shared` events to different controllers, so I used constraint objects
to separate the requests.

```ruby
# config/routes.rb

post "slack", to: "slack/url_verifications#create",
              constraints: SlackUrlVerificationConstraint.new

post "slack", to: "slack/unfurlings#create",
              constraints: SlackLinkSharedConstraint.new
```

```ruby
# app/models/slack_url_verification_constraint.rb

class SlackUrlVerificationConstraint
  def matches?(request)
    request.params[:type] == "url_verification"
  end
end
```

```ruby
# app/models/slack_link_shared_constraint.rb

class SlackLinkSharedConstraint
  def matches?(request)
    event_callback?(request) && link_shared?(request)
  end

  private

  def event_callback?(request)
    request.params[:type] == "event_callback"
  end

  def link_shared?(request)
    request.params.dig(:event, :type) == "link_shared"
  end
end
```

I'm not the biggest fan of the resulting routes, but I *really* like handling
different event types in different controllers. I'm excited to keep
experimenting with this approach!
