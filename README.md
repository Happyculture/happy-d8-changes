Et maintenant en Drupal 8 comment je fais ?
===========================================

Voici une liste (non exhaustive) de fonctions utilisées couramment dans Drupal 7 et ce qui leur arrive dans Drupal 8. Vous trouverez dans la plupart des éléments de cette liste le(s) "change record(s)" associé(s) (l'annonce du changement et ses conséquences https://www.drupal.org/list-changes).

### Ce qui ne change pas, ou peu

**t**() existe encore mais fait appel à **\Drupal::translation**()->**translate**($string, $args, $options);

**drupal_get_path**() est inchangée

**drupal_set_message**() existe encore

**drupal_debug**() est inchangée

**format_string**() existe encore mais fait appel à **String::format**($string, $args); https://www.drupal.org/node/2302363

**watchdog**($type, $message, $variables, $severity, $link) existe encore mais fait appel au service de logging via : **\Drupal::service**('logger.factory')->**get**($type)->**log**($severity, $message, $variables);

**drupal_static**() est inchangée

Dans le **hook_theme()**, lorsque l'on spécifie un template, l'emplacement du template a déjà pour préfixe "templates/".

### Ce qui a été remplacé

**url**() est remplacé par des factory **Url::fromRoute**() et **Url::fromUri**() https://www.drupal.org/node/2346779

**l**() est remplacé par **\Drupal::l**() https://www.drupal.org/node/2346779

**user_access**() est remplacé par la méthode **hasPermission**() de la class AccountInterface. https://www.drupal.org/node/2049309

**theme**() est remplacé par la construction d'un render array et l'appel à **drupal_render**() https://www.drupal.org/node/2195739

**drupal_add_css**(), **drupal_add_js**() and **drupal_add_library**() sont remplacés par un rajout des infos dans le '#attached' d'un render_array https://www.drupal.org/node/2169605

**global $user** est remplacé par **\Drupal::currentUser**() https://www.drupal.org/node/2032447

**global $lang** est remplacé par **\Drupal::languageManager**()->**getLanguage**()  https://www.drupal.org/node/1450578

**check_plain**() est remplacé par **String::checkPlain**() https://www.drupal.org/node/2302363

**filter_xss**() est remplacé par le composant Xss, $safe = **Xss::filter**($string); https://www.drupal.org/node/2239919

**node_load**() est remplacé par **EntityInterface::load**() https://www.drupal.org/node/2266845

**form_set_error**() est remplacé par **setErrorByName**() https://www.drupal.org/node/2186135 et https://www.drupal.org/node/2142817

**system_settings_form**() est remplacé par l'extension de la class ConfigFormBase https://www.drupal.org/node/1910694

**variable_get**(), **variable_set**(), **variable_del**() sont remplacés par l'api de configuration https://www.drupal.org/node/2183531 et https://www.drupal.org/node/1809490

**drupal_access_denied**() est remplacé par throw new AccessDeniedHttpException(); venant du httpKernel Symfony https://www.drupal.org/node/1616360
Dans le même esprit **drupal_not_found**() est remplacé par throw new NotFoundHttpException();

**drupal_get_title**() est remplacé par le service 'title_resolver' https://www.drupal.org/node/2067859
**drupal_set_title**() par la définition du titre dans le fichier de routes https://www.drupal.org/node/2067859

**module_exists**() est remplacé par **\Drupal::moduleHandler**()->**moduleExists**($module). De plus la pluspart des fonctions systèmes lié aux modules sont remplacés par cette class moduleHandler https://www.drupal.org/node/1894902.

**drupal_goto**() a été supprimé en faveur de la class RedirectResponse  https://www.drupal.org/node/2023537

**cache_get**(), **cache_set**() sont remplacés par la Cache factory https://www.drupal.org/node/1272696

**drush cache-clear all** (drush cc all) est remplacé par **drush cache-rebuild** (drush cr)

**path_to_theme**() est remplacé par un objet ActiveTheme et la methode getPath **\Drupal::theme**()->**getActiveTheme**()->**getPath**(); https://www.drupal.org/node/2324935

**drupal_mail**() est remplacé par la méthode **MailManagerInterface::mail**() appelé ainsi : **\Drupal::service**('plugin.manager.mail')->**mail**($module, $key, $to, $langcode); https://www.drupal.org/node/2309379

**drupal_get_form**() est remplacé par un service **\Drupal::formBuilder**()->**getForm**()

### Ce qui n'existe plus

$_GET['q'] n'existe plus il faut utiliser **current_path**() (mais c'était déjà une bonne pratique Drupal 7) https://www.drupal.org/node/1659562
