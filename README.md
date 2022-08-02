# Vtiger Composer

> What it Composer?

Composer is a dependency manager and autoloading expert for PHP.

Have you heard about or used npm? (or yarn) Or if you’re a Rubyist, Bundler must not be new to you. Composer provides similar functionality for the PHP world. It used to be PEAR (PHP Extension and Application Repository) in early days.

One important thing to note here is that the open-source packages generally recide on Packagist and composer downloads the dependencies from there, unless you specify other location. Packagist, in turn, keep and updates the code from Git/Svn repositories. And you can also use private repository with composer by using Private packagist or hosting them yourself.

I hate theory. Let’s have some practical talk.

> Pains that Composer fixes

Following are some of pains that Composer has relieved:

When you are working on a new project using a framework, you depend on it’s updates. As they release new versions with bug fixes and new features, you should keep the framework updated for security, performance, and other reasons.

But, it’s a pain to manually download it everytime, replace the existing files and test things again. It takes time. And that is why there are so many old codebases relying on the versions of frameworks that are no longer supported. Working on legacy projects is something that all of us try to avoid, isn’t it?

Pre-composer days, the size of the project directory used to be very big. We would carry all the libraries that our project depends on and pass around the project either in USB sticks or pollute the VCS (git) history.

Enter Composer – Size reduces to less than 20%? We can get away without keeping the dependencies in the project (.gitignore) and avoid version mismatches at the same time thanks to composer.lock file.

sad fact – Codeigniter 3 still uses the traditional download system.

> Hours of debugging

The libraries or frameworks that your project uses depend on some other libraries (and the chain continues…). Possibly, the framework is using version X of a library while another library is using version Y of the same library.

You have been getting errors due to some clash or incompatibilty and have to put a lot of time to get to the base of the issue. No more – composer keeps only one copy of a library with a suitable version or denies the installation request.

> Autoloading

Remember that long list require statements? As the project grows in size, so does the number of files we need to include in each of the file. PHP autoloading came to the rescue but still it was comparatively hard to setup and maintain as dependencies grow. Less discussed powerful feature of Composer is Autoloading. It supports PSR-0, PSR-4, class mapping as well as files autoloading. We need to require just one file and we’re done. Play with straightforward namespaces and enjoy the development time.

Less known fact – Composer provides three different levels of autoloader optimisation for your different level of needs.

Often times, one or more steps need to be followed after downloading a library for setup and installation. Package maintainers had to write detailed installation procedures in the documentation and still answer support queries when users won’t follow them and then complain about errors. Composer scripts are a boon for them.

One can easily code the steps that can be automated and run as a script during various stages of the package download. For example, Laravel uses composer scripts to create an .env file, create an application key, and perform automatic discovery of the packages.

> Platform Requirements

The code of your library/package may support only latest PHP versions or depend on specific PHP extensions. And you can inform Composer about this resulting in prevention of package downloads on the systems that don’t meet the requirements. For example,

```
"require": {
    "php": "^7.1.3",
    "ext-mbstring": "*",
    "ext-openssl": "*",
    ...
},
```

Add this to your composer.json and composer will throw an error when the systems with PHP less than v7.1.3 or without mbstring and openssl extension try to download the package.

> Maintaining a library/package

Package maintainers had to either maintain different directories for each version of the package or release new versions through GitHub everytime there was an important update. Thanks to the graceful integration of Composer with VCS tags and branches, one just needs to add a tag to the commit and push. The rest is taken care of.

Composer highly recommends Semantic Versioning and following that, package maintainers can keep focus on actual development without worrying about the distribution.

Marvellous. I do not have complains any more and am ready to jump in. What next?

> Version management

Understanding how composer downloads the libraries based on the version constraints specified in your composer.json file will help you a long way. I recommend you to go through the original documentation article at least once.

Did you know? – You can require a package by its version, branch or
even by a specific commit SHA (not recommended).

Personally, my suggestion is to use Caret Version Range () for the packages which use Semantic versioning and Wildcard Version Range (.*) for others as they are easy to grasp.

