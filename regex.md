// A mettre au début du php : permet de modifier toutes les dates en français
// Il faudra appliquer la fonction à la date voulue

/* Configure le script en français */
setlocale (LC_TIME, 'fr_FR.UTF8','fra');
//Définit le décalage horaire par défaut de toutes les fonctions date/heure  
date_default_timezone_set("Europe/Paris");
//Convertir une date US en françcais
function dateFr($date){
return strftime('%A %d %B %Y, %H:%M:%S',strtotime($date));
}



Mémo regex

Pour la civilité :

regexGender = /^(Monsieur|Madame|Autre)$/;

Pour les nom :

// 1) Si vous différienciez nom et prénom dans 2 input différents, cette régex conviendra parfaitement.
// Elle accepte un nom simple ou composé, compris entre 2 et 17 caractère, reliés par un espace,
// un tiret ou une apostrophe (pour les irlandais ;)
regexName = /^[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç\']{2,17}[- \']?[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç]{0,17}$/;

// 2) Si vous voulez que l'on mette nom et prénom dans une seule input, il faudra utiliser cette regex.
// Elle accepte les prénoms composés + particule + nom composé.
// Ex : Marie-Claire des Champs-Vallon
// Et tout ce qui est plus petit.
regexFirstNameLastName = /^[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç']{0,17}[- ']?[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç']{0,17}[ ]?[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç']{0,3}[ ]?[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç']{2,17}[- ']?[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç']{0,17}$/


Pour les adresses mails :

// A rajouter en plus du type mail, car plus élaboré encore.
regexMail = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/


Pour les dates :

//1) Si vous utilisez un type="date", cette regex permet de vérifier la conversion de l'ordinateur
// qui reçoit votre date au format US, bien que vous l'ayez rentrée au format fr.
regexDate = /^([12]\d{3}-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01]))$/;

// 2) Méthode pour transformer la date réceptionnée par l'ordi en format US et l'afficher en format fr (en JQuery).
var date = $("#date").val();
var event = new Date(date);
var options = { weekday: "long", year: "numeric", month: "long", day: "numeric" };
var frenchDate = event.toLocaleDateString("fr-FR", options);

Pour les calendrier :

// Prends en compte les années bisextiles.
regexCalendar = ^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]))\g1|(?:(?:29|30)(\/|-|\.)(?:0?[13-9]|1[0-2])\g2))(?:(?:1[6-9]|[2-9]\d)?\d{2})$|^(?:29(\/|-|\.)0?2\g3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)(?:(?:0?[1-9])|(?:1[0-2]))\g4(?:(?:1[6-9]|[2-9]\d)?\d{2})$

Pour les heures :

regexHour = ^([0-1][0-9]:[0-5][0-9]:[0-5][0-9])|(2[0-3]:[0-5][0-9]:[0-5][0-9])$/;


Pour le numéro de téléphone, en indiquant le +33 dans votre label, remplaçant ainsi le premier 0 (numéro international) :

// 1) Uniquement les chiffre collés.
regexPhone = /^[0-9]{9}$/;

// 2) Avec la possibilité de séparer par un point, un espace ou un tiret, ou en les collant, ou en ajoutant "+33" à la place du zéro.
regexPhone = /^[+][3]{2}[1-9]([-. ]?)(([0-9]{2})\g1([0-9]{2}))(\g1([0-9]{2})){2}|[0][1-9]([-. ]?)(([0-9]{2})\g7([0-9]{2}))(\g7([0-9]{2})){2}$/;


Pour récupérer une adresse postale :

// 1) Le nom de la rue :
regexStreet = /^(avenue|Avenue|AVENUE|rue|Rue|RUE|Boulevard|BOULEVARD|boulevard|Impasse|IMPASSE|impasse|Allée|ALLEE|allée|hameau|Hameau|HAMEAU|Chemin|chemin|CHEMIN|lieu-dit|Lieu-dit|LIEU-DIT|lieu-Dit|Lieu-Dit)[- ][A-Za-zéèàâêŷûîôäëïöüÿùç]+([- ]?[A-Za-zéèàâêŷûîôäëïöüÿùç]{0,17}){0,3}$/;

// 2) Le numéro de la rue :
regexStreetNumber = /^([1-9]|[1-9][0-9]|[1-9][0-9]{2}|1[0-9]{3})[A|a|B|b]?[ ]?(bis)?$/;

// 3) numéro de rue + nom de rue :
regexAddress = /^([1-9]|[1-9][0-9]|[1-9][0-9]{2}|1[0-9]{3})[A|a|B|b]?[ ]?(bis)?[- ](avenue|Avenue|AVENUE|rue|Rue|RUE|Boulevard|BOULEVARD|boulevard|Impasse|IMPASSE|impasse|Allée|ALLEE|allée|hameau|Hameau|HAMEAU|Chemin|chemin|CHEMIN|lieu-dit|Lieu-dit|LIEU-DIT|lieu-Dit|Lieu-Dit)[- ][A-Za-zéèàâêŷûîôäëïöüÿùç]+([- ]?[A-Za-zéèàâêŷûîôäëïöüÿùç]{0,17}){0,3}$/;

// 4) Le code postal correspondant au territoire français (métropole + DOM-TOM)
regexPostal = /^((0[1-9]|[1-8][0-9]|9[0-5])[0-9]{3})|97[1-6]$/;

// 5) La première regexName fonctionne très bien pour le nom de la ville.
regexCity = /^[A-Za-zéèàâêŷûîôäëïöüÿùç]+([- ]?[A-Za-zéèàâêŷûîôäëïöüÿùç]{0,17}){0,10}$/;

Pour le login/identifiant :
// Sur la base de la regexName, on rajoute l'utilisation des chiffres et des caractères spéciaux. Simplement on limite la taille à 2 fois 15 caractères max.

regexLogin = /^[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç0-9œ&~#{([|_\^@)°+=}$£*µ%!§.;,?<>]{2,15}[- ']?[a-zA-ZéèÉÈôîêûÛÊÔÎùÙïöëüËÏÖÜç0-9œ&~#{([|_\^@)°+=}$£*µ%!§.;,?<>]{0,15}$/;

Pour un mot de passe secure :

// Le mot de passe devra faire entre 8 et 15 caractères, contenant au moins une minuscule et une majuscule, ainsi qu'un chiffre et un caractère spécial.
regexPassword = /^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[-+!*$@%_.])([-.+!*$@%_\w]{8,15})$/;


Pour les cartes bancaires :

// 1) Exemple acceptant 5 types de cartes : Visa, MasterCard, American Express, Diners Club, Discover, et JCB cards.
regexCB = /^(?:[0-9]{12}|[25][1-7][0-9]{14}|6(?:011|5[0-9][0-9])[0-9]{12}|3[47][0-9]{13}|3(?:0[0-5]|[68][0-9])[0-9]{11}|(?:2131|1800|35\d{3})\d{11}|\s)$/;

// 2) Le code de sécurité au verso (si nécessaire, selon la carte).
regexCryptoCB = /^[0-9]{3}$/;

Pour l'URL :

$regexURL = " #^(?:(?:https?|ftp):\/\/)(?:\S+(?::\S*)?@|\d{1,3}(?:\.\d{1,3}){3}|(?:(?:[a-z\d]+-?)*[a-z\d]+)(?:\.(?:[a-z\d]+-?)*[a-z\d]+)*(?:\.[a-z]{2,6}))(?::\d+)?(?:[^\s]*)?$# ";

ou

/^(https?://(?:www.|(?!www))[a-zA-Z0-9][a-zA-Z0-9-]+[a-zA-Z0-9].[^\s]{2,}|www.[a-zA-Z0-9][a-zA-Z0-9-]+[a-zA-Z0-9].[^\s]{2,}|https?://(?:www.|(?!www))[a-zA-Z0-9]+.[^\s]{2,}|www.[a-zA-Z0-9]+.[^\s]{2,})$/;

Pour mettre l'ensemble des valeurs d'un tableau en regex :
// Exemple pour un select qui demanderait de sélectionner son pays
$country = implode('|',$countryCode); // $countryCode étant le nom du tableau
            $regexCountry = "/^(".$country.")$/";


Pour Pôle Emploi :

regexPE = /^[0-9]{8}|[0-9]{7}[A-Z]{1}|[0-9]{3}[ ][0-9]{3}[ ][0-9]{2}|[0-9]{3}[ ][0-9]{3}[ ][0-9]{1}[A-Z]{1}|[0-9]{12}|[0-9]{3}[ ][0-9]{3}[ ][0-9]{3}[ ][0-9]{2}[A-Z]{1}|[0-9]{3}[ ][0-9]{3}[ ][0-9]{3}[ ][0-9]{3}|[0-9]{11}[A-Z]{1}|[0-9]{12}$/;


Pour l'âge :

// De 16 à 123 ans
regexAge = " /^1[6-9][ ]?(ans|ANS|Ans)?$|^[2-9][0-9][ ]?(ans|ANS|Ans)?$|^1[0-1][0-9][ ]?(ans|ANS|Ans)?$|^12[0-3]$/ ";
