# util.js

A very basic framework extending browser API's. Provides extended `Element`, ajax requests & an `.each` function.


## util.Element

util.Element objects are extended `Element` objects, so all the in-built browser functions work alongside the util.js specific ones. They can be accessed via `util.element` and `util.elements`. Most of the util.js functions are merely wrappers around the browser equivilents, the advantage being able to chain up functions:

	util.element( 'body' ).addClass( 'orange' ).css({ 'margin-top': '30px' });
		

## util.build & util.Element.buildThese functions allow you to create and append elements to each other.

    var $table = util.element( 'body' ).build( 'table' )
        .build( 'thead' )
            .build( 'tr' )
                .each( [ 'id', 'header 1', 'header 2', 'header 3' ], function( key, value ) {
                    this.build( 'th' ).innerHTML = value;
                })
            .parentNode
        .parentNode
        .build( 'tbody' )
            .each( [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ], function( key, value ) {
                var $tr = this.build( 'tr' )
                    .build( 'td' ).set( 'innerHTML', value ).parentNode;
                $tr.each( [ 'content 1', 'content 2', 'content 3' ], function( key, value ) {
                    this.build( 'td' ).innerHTML = value;
                });
            })
        .parentNode;