---
layout: default
title: AutoMapper & AutoFac
type: post
status: publish
published: true
---

#### Prelude
So I tend to develop things in the way of

1. Make it work
2. Make it pretty

#### Make it work
So when using [AutoMapper](http://automapper.org/) after step one I ended up with something like this
{% highlight csharp %}
.ForMember(d => d.SomeSource, 
     o => o.MapFrom(
          s => new Serializer().Deserialize<SomeViewModel>(s.Serialized)))
{% endhighlight %}
Some background, for the destination SomeSource I needed to Deserialize the value as it was currently stored as Json in my database.

#### Make it pretty
While it works it looks rather horrible, so I started looking into something that allowed me to get a ISerializer from [AutoFac](http://autofac.org/) (my [IoC](http://en.wikipedia.org/wiki/Inversion_of_control) of choice) instead.

So, first I added a custom ValueResolver that looked like this
{% highlight csharp %}
public class SomeViewModelResolver 
    : ValueResolver<OrderRow, ScheduleViewModel>
    {
        private readonly ISerializer _serializer;

        public ScheduleViewModelResolver(ISerializer serializer)
        {
            _serializer = serializer;
        }

        protected override SomeViewModel ResolveCore(Source source)
        {
            return _serializer.Deserialize<SomeViewModel>(source.Serialized);
        }
    }
{% endhighlight %}
Next was to connect AutoMapper with AutoFac and to register the ValueResolver:
{% highlight csharp %}
// Register my new valueresolver
builder.RegisterType<SomeViewModelResolver>();

// Connect AutoMapper to AutoFac
Mapper.Initialize(x => x.ConstructServicesUsing(container.Resolve));
{% endhighlight %}
Once that is done the last thing to change is to modify the ForMember call to use the new ValueResolver instead
{% highlight csharp %}
.ForMember(d => d.SomeSource, o => o.ResolveUsing<SomeViewModelResolver>())
{% endhighlight %}
Looks a lot cleaner and follows the flow that you would expect when using a IoC container.

#### Bonus
If you don't want to have calls to the static ``Mapper.Map<>`` all over your code, it is possible to register the IMappingEngine in AutoMapper in you IoC container and have that as an dependency for you class too. For AutoFac the registration looks like this
{% highlight csharp %}
builder.Register(c => Mapper.Engine).As<IMappingEngine>().SingleInstance();
{% endhighlight %}
The important thing is to register it as a [singelton](http://en.wikipedia.org/wiki/Singleton_pattern). Once that is done just add ``IMappingEngine mappingEngine`` to the constructors of those classes that use AutomMapper.