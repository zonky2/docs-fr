.. _rst_cookbook_tips_delete_child_items:

Suppression automatique des enregistrements dans les tables enfants
=========================================================================

Lorsque des tables sont liées dans MetaModels en tant que tables enfants, les enregistrements (enfants) ne sont
actuellement pas supprimés automatiquement lorsque l'enregistrement parent correspondant est supprimé. Le DC_General
prend certes en charge la fonction « deep delete », mais celle-ci n'est pas encore activable par configuration pour
ses propres tables dans MM.

Elle peut cependant être mise en place avec une configuration DCA dédiée pour chaque relation parent-enfant. Cela
signifie également que la suppression peut être activée pour des relations parent-enfant-enfant. À chaque niveau, un
fichier doit être créé, qui doit contenir en conséquence tous les niveaux « inférieurs ».

L'exemple suivant concerne la hiérarchie à deux niveaux des tables MM `mm_parent` avec `mm_child` ainsi que
`mm_child_child`. Selon la version de Contao, les fichiers DCA doivent être placés dans les dossiers correspondants
- pour Contao 4.9 par ex. dans `contao/dca` (voir le `manuel Contao <https://docs.contao.org/dev/framework/dca/>`_).

.. code-block:: php
   :linenos:

    <?php
    // contao/dca/mm_parent.php
    $GLOBALS['TL_DCA']['mm_parent'] = [
        'dca_config' => [
            'data_provider'  => [
                'default' => [
                    'source' => 'mm_parent'
                ],
                'mm_child' => [
                    'source' => 'mm_child'
                ],
                'mm_child_child' => [
                    'source' => 'mm_child_child'
                ],
            ],
            'childCondition' => [
                [
                    'from'    => 'mm_parent',
                    'to'      => 'mm_child',
                    'setOn'   => [
                        [
                            'to_field'   => 'pid',
                            'from_field' => 'id',
                        ],
                    ],
                    'filter'  => [
                        [
                            'local'     => 'pid',
                            'remote'    => 'id',
                            'operation' => '=',
                        ],
                    ],
                    'inverse' => [
                        [
                            'local'     => 'pid',
                            'remote'    => 'id',
                            'operation' => '=',
                        ],
                    ]
                ],
                [
                    'from'    => 'mm_child',
                    'to'      => 'mm_child_child',
                    'setOn'   => [
                        [
                            'to_field'   => 'pid',
                            'from_field' => 'id',
                        ],
                    ],
                    'filter'  => [
                        [
                            'local'     => 'pid',
                            'remote'    => 'id',
                            'operation' => '=',
                        ],
                    ],
                    'inverse' => [
                        [
                            'local'     => 'pid',
                            'remote'    => 'id',
                            'operation' => '=',
                        ],
                    ]
                ],
            ],
        ]
    ];

.. code-block:: php
   :linenos:

    <?php
    // contao/dca/mm_child.php
    $GLOBALS['TL_DCA']['mm_child'] = [
        'dca_config' => [
            'data_provider'  => [
                'default' => [
                    'source' => 'mm_child'
                ],
                'mm_child_child' => [
                    'source' => 'mm_child_child'
                ],
            ],
            'childCondition' => [
                [
                    'from'    => 'mm_child',
                    'to'      => 'mm_child_child',
                    'setOn'   => [
                        [
                            'to_field'   => 'pid',
                            'from_field' => 'id',
                        ],
                    ],
                    'filter'  => [
                        [
                            'local'     => 'pid',
                            'remote'    => 'id',
                            'operation' => '=',
                        ],
                    ],
                    'inverse' => [
                        [
                            'local'     => 'pid',
                            'remote'    => 'id',
                            'operation' => '=',
                        ],
                    ]
                ],
            ],
        ]
    ];

Malheureusement, l'édition en frontend (FEE) ne prend pas encore en charge la relation avec les tables enfants, de
sorte qu'une routine de suppression dédiée doit être créée ici. Pour le déclenchement, on pourrait par exemple
utiliser le `PostDeleteModelEvent <https://github.com/contao-community-alliance/dc-general/blob/61ffe2081323104b38ad951b2fbb3cb4b0f1a025/src/Event/PostDeleteModelEvent.php>`_
du DC_G. Avec l'ID du modèle supprimé, tous les enregistrements enfants ayant la même PID peuvent être trouvés et
supprimés.

Si l'édition ou la suppression d'un item MM se fait via un formulaire, une routine de suppression doit y être
intégrée.

.. |br| raw:: html

   <br />
