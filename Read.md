# Trabalho_Pratico_de_Tecnicas_DEV_IPCA

# Plataformer2D

### Este projeto é sobre a analíse de um jogo Platformer 2D desenvolvido em monogame e em C#

---

Grupo

João Sousa a25613

João Pereira a25967

Gustavo Antunes a25983

---

# Estrutura do Código

##### Uma vez que o jogo foi desenvolvido em C#, o código está dividido em classes:

1. PlatformerGame.cs

2. Accelerometer.cs

3. Animation.cs

4. AnimationPlayer.cs

5. Circle.cs

6. Enemy.cs

7. Gem.cs

8. Level.cs

9. Player.cs

10. RectangleExtensions.cs

11. Tile.cs

12. TouchCollectionExtensions.cs

13. VirtualGamePad.cs

____

## Análise das diversas classes

##### PlatformerGame

Esta é a classe principal do jogo. O jogo usa o Microsoft XNA Community Game Platform, que é uma estrutura de jogos usada para desenvolver jogos para Windows, Xbox 360 e Windows Phone.

A classe `PlatformerGame` contém recursos e variáveis ​​que lidam com desenho, estado de jogo, input do jogador e o carregamento de conteúdo de jogos, incluindo fontes, texturas e sons.

O jogo tem vários níveis que são armazenados como arquivos num diretório do conteúdo do jogo. A classe lê esses arquivos e carrega-os para o jogo.

A classe também inclui um método `Update` que é chamado uma vez a cada frame do jogo. Neste método, o estado do jogo é atualizado e verifica se o jogador concluiu o nível ou perdeu o jogo.

Além disso, o código também inclui um método `LoadContent` que é chamado apenas uma vez no início do jogo e é usado para carregar todo o conteúdo do jogo.

Algumas partes do código são específicas para o XNA, como a classe `SpriteBatch` usada para desenhar texturas na tela e as classes de entrada de jogo, como `GamePadState` e `KeyboardState`, usadas para receber o input do jogador.

____

##### Accelerometer

Esta é uma classe estática chamada `Accelerometer` que contêm também  uma struct chamada `AccelerometerState`. O objetivo desta classe é encapsular a entrada do acelerômetro para fornecer um sistema de acelerômetro baseado em polling para jogos.

A classe `Accelerometer` possui dois métodos: `Initialize` e `GetState`. O método `Initialize` é responsável por inicializar o acelerômetro para o jogo atual. Ele verifica se o acelerômetro já foi inicializado anteriormente para evitar inicializações repetidas. Já o método `GetState` é responsável por retornar o estado atual do acelerômetro. Ele verifica se o acelerômetro foi inicializado antes de tentar obter o estado. O método retorna um novo objeto `AccelerometerState` com o estado atual do acelerômetro.

A struct `AccelerometerState` contém duas propriedades: `Acceleration` e `IsActive`. A propriedade `Acceleration` armazena a aceleração atual do acelerômetro em unidades de G-force. A propriedade `IsActive` indica se o acelerômetro está ativo e em execução.

____

##### Animation

Esta classe contém propriedades que representam os aspectos básicos de uma animação, como a textura (ou imagem) que contém todos os framwa da animação, o tempo que cada frame deve ser exibido, se a animação deve ou não se repetir em um loop, o número de frames na animação e a largura e altura de cada frame.

Além disso, a classe também tem um construtor que recebe a textura, o tempo de exibição de cada frame e um flag que indica se a animação deve se repetir em um loop. O construtor é responsável por inicializar as propriedades da classe com os valores passados como argumentos.

____

##### AnimationPlayer

Esta classe contém uma estrutura chamada `AnimationPlayer` que controla a reprodução das  animações que aparecem na classe `Animation`. 

A estrutura `AnimationPlayer` tem as seguintes propriedades e métodos:

- A propriedade `Animation` retorna a animação atualmente em reprodução.
- A propriedade `FrameIndex` retorna o índice do frame atual na animação.
- A propriedade `Origin` retorna a origem da textura para cada frame, que é no centro inferior.
- O método `PlayAnimation` inicia ou continua a reprodução de uma animação.
- O método `Draw` avança a posição de tempo e desenha o frame atual da animação na tela.

O método `Draw` desenha a imagem usando o objeto `SpriteBatch`, que é uma classe fornecida pela plataforma XNA que permite desenhar imagens 2D na tela. O código usa a propriedade `ElapsedGameTime` do objeto `GameTime` para avançar o tempo de exibição de cada frame da animação. Se a animação estiver em loop, o índice do frame é incrementado e mantido dentro dos limites da animação. Caso contrário, o índice do frame é incrementado uma vez e, em seguida, é mantido como o último frame na animação. Finalmente, o código usa a função `Draw` do objeto `SpriteBatch` para desenhar o frame atual da animação na posição especificada na tela, com a rotação e a escala definidas como padrão.

____

##### Circle

Esta classe define a estrutura `Circle`  .

A estrutura `Circle` possui dois campos: um Vector2 (`Center`) que representa a posição central do círculo no espaço 2D e um float (`Radius`) que representa o raio do círculo.

O construtor da estrutura recebe um Vector2 (`position`) e um float (`radius`) e utiliza-os para inicializar os campos `Center` e `Radius` da estrutura.

O método `Intersects(Rectangle rectangle)` determina se um círculo intersecta um retângulo e retorna um valor booleano (True ou False). Ele utiliza a posição central e o raio do círculo para calcular se ele intersecta o retângulo recebido como parâmetro. Para fazer isso, ele encontra primeiro o ponto mais próximo da posição central do círculo dentro do retângulo (`v`). Em seguida, ele calcula a distância entre o ponto mais próximo e o centro do círculo (`direction`) e verifica se a distância é menor que o raio do círculo (`Radius`). Se for, então o círculo intersecta o retângulo e o método retorna True, caso contrário, retorna False.

___

##### Enemy

o enum `FaceDirection` que representa a direção em que um objeto está virado na tela. Existem apenas dois valores possíveis: `Left` (esquerda) e `Right` (direita).

`Level` uma referência à instância da classe `Level` que contém esse monstro. É útil para que o monstro possa interagir com outros objetos no jogo.

`Position` representa a posição desse monstro no espaço do mundo do jogo. A posição é um vetor de duas dimensões (`Vector2`).

`BoundingRectangle` representa o retângulo que circunda esse monstro no espaço do mundo do jogo. O retângulo é calculado a partir da posição do monstro e do tamanho da sua sprite.

Essas variáveis representam as animações que o monstro pode ter. A `runAnimation` representa a animação de movimento do monstro e a `idleAnimation` representa a animação quando o monstro está parado. A `sprite` é uma instância da classe `AnimationPlayer` que gerencia a animação atual do monstro.

Aqui é declarada uma variável `direction` que armazena a direção em que o monstro está virado. Ela é inicializada com o valor `Left` (esquerda) por padrão.

`waitTime` : guarda quanto tempo o inimigo deve esperar antes de se virar.

`MaxWaitTime` : guarda o tempo máximo de espera antes de o inimigo se virar. Este valor é constante e não pode ser alterado.

`MoveSpeed` : guarda a velocidade de movimento do inimigo ao longo do eixo X. Este valor também é constante.

Contrução de um novo inimigo

Carrega os sprite e sons de um inimigo específico.

Primeiramente, é adicionado o caminho ("Sprites/" + spriteSet + "/") ao nome do spriteSet, para indicar que os arquivos estão localizados em uma pasta específica.

Em seguida, são criados objetos `Animation` a partir dos arquivos de imagem carregados com `Content.Load()`. Estes objetos são passados para os campos `runAnimation` e `idleAnimation` da classe `Enemy`. O primeiro parâmetro do construtor de `Animation` é a textura carregada, o segundo é o tempo de exibição de cada quadro da animação e o terceiro indica se a animação deve ser executada em loop.

Por fim, é calculado um retângulo de limites locais (`localBounds`) para a área do sprite que representa o inimigo. Esse retângulo é usado para detectar colisões com outros objetos no jogo. O tamanho e posição do retângulo é definido como uma fração da largura e altura do quadro da animação "Idle". Os valores específicos para `width`, `left`, `height` e `top` são calculados para posicionar o retângulo no sprite de maneira que ele englobe apenas a área relevante para a colisão.

No início do método, é calculado o tempo decorrido desde o último quadro de jogo. Em seguida, é calculada a posição do inimigo em relação à sua direção atual e à largura da área de colisão do inimigo.

A seguir, é verificado se o inimigo está esperando. Se sim, o tempo de espera é reduzido pelo tempo decorrido desde o último quadro de jogo. Se o tempo de espera chegar a zero, o inimigo se vira e muda sua direção.

Se o inimigo não está esperando, é verificado se ele está prestes a colidir com uma parede ou cair de um penhasco. Se sim, o tempo de espera é definido como o tempo máximo de espera (MaxWaitTime). Se não, o inimigo é movido na direção atual com uma velocidade predefinida (MoveSpeed).

Em resumo, este método implementa o comportamento de movimentação do inimigo, que anda de um lado para o outro em uma plataforma, espera nos extremos da plataforma e se vira quando encontra uma parede ou um penhasco.

Se o jogo estiver pausado, se o jogador não estiver vivo, se o nível foi concluído ou se o inimigo está esperando para mudar de direção, a animação do inimigo será definida como idle (parado). Caso contrário, a animação será definida como run (correr).

Em seguida, o inimigo é desenhado na direção em que está se movendo. Se a direção for maior que zero (ou seja, se estiver se movendo para a direita), o sprite é desenhado sem alterações. Caso contrário, o sprite é espelhado horizontalmente usando o parâmetro flip.

O método recebe como parâmetros o gameTime e o spriteBatch, que é usado para desenhar o sprite do inimigo na tela.

___

##### Gem

`Texture2D texture`: representa a textura (imagem) que será usada para desenhar a gema.

`Vector2 origin`: representa a origem da textura, ou seja, o ponto no qual a textura será desenhada em relação à posição da gema.

`SoundEffect collectedSound`: representa o efeito sonoro que será reproduzido quando a gema for coletada.

`int PointValue`: é uma propriedade somente leitura que define o valor da gema em pontos. Neste caso, o valor é fixo em 30 pontos.

`Color Color`: é uma propriedade somente leitura que define a cor da gema. Neste caso, a cor é amarela.

A "gem" é animada a partir de uma posição base ao longo do eixo Y. A variável "basePosition" armazena essa posição base, enquanto a variável "bounce" armazena a altura da animação de "bounce" da "gem". A propriedade "Level" é usada para armazenar o objeto "Level" ao qual a "gem" pertence. A propriedade "get" retorna o valor da variável "level".

Obtém a posição atual desta joia no espaço.

Obtém um círculo que limita esta joia no espaço.

Constrói uma nova gema.

Carrega a textura da gema e o som qualdo é coletada.

Este trecho de código faz com que a gema ("gem") salte para cima e para baixo no ar para atrair os jogadores a coletá-las.

Existem três constantes que controlam a altura e a taxa de salto da gema: "BounceHeight", "BounceRate" e "BounceSync". Essas constantes afetam a forma como a gema salta no jogo.

O método "Update" é chamado uma vez a cada quadro do jogo e atualiza o estado da gema. Ele usa as constantes mencionadas acima para fazer a gema saltar ao longo de uma curva senoide no tempo. A posição X da gema é incluída para que as gemas vizinhas saltem em um padrão de onda agradável. O resultado final é armazenado na variável "bounce", que é usada na propriedade "Position" para calcular a posição atual da gema em relação à sua posição base.

A função `OnCollected` é chamada quando o jogador coleta a gema e é removida do nível. Ela reproduz o som de uma gema sendo coletada.

A função `Draw` é responsável por desenhar a gema na tela. Ela usa o objeto `SpriteBatch` para desenhar a textura da gema na posição atual, que é obtida da propriedade `Position`. A cor da gema é definida pela propriedade `Color`, e a origem do desenho é definida pela propriedade `origin`. A escala do desenho é definida como 1.0f e não há efeito de espelhamento aplicado. O parâmetro `SpriteEffects` é definido como `None`, e o parâmetro `layerDepth` é definido como 0.0f.

Este trecho de código define a estrutura física de um nível do jogo, incluindo as camadas de texturas, as entidades (jogador, inimigos e gemas), as posições importantes (ponto de partida, saída), o estado do jogo (pontuação, tempo restante, se o jogador alcançou a saída) e o conteúdo do nível (incluindo o gerenciador de conteúdo do jogo e o som a ser reproduzido quando o jogador alcançar a saída).

Em particular, o código define um array de Tiles bidimensional para a estrutura física do nível, um array de texturas para as diferentes camadas do nível, uma constante que indica a camada em que as entidades são desenhadas, uma lista de objetos Gem que representam as gemas no nível, uma lista de objetos Enemy que representam os inimigos no nível e objetos Vector2 e Point para as posições de partida e saída no nível. O estado do jogo é armazenado em variáveis como score (pontuação), reachedExit (se o jogador alcançou a saída) e timeRemaining (tempo restante). O código também inclui um objeto Random para gerar valores aleatórios no jogo e um objeto ContentManager para gerenciar o conteúdo do nível, incluindo o som que será reproduzido quando o jogador alcançar a saída.

____

##### Level

Na classe `Level` o codigo esta dividio em mais 4 partes `loding`,`Bounds and collision`, `Update`, `Draw`.

**loading**

Este código pertence a uma classe `Level` que é responsável por criar um nível no jogo. O construtor da classe `Level` recebe um `IServiceProvider` e um `Stream` que contém os dados do mapa, bem como um índice para identificar qual nível deve ser carregado. O construtor é responsável por carregar as texturas do fundo, e os sons que serão usados no nível.

O método `LoadTiles` lê os dados do mapa que são fornecidos pelo `Stream` e carrega as texturas de cada um dos tiles do nível. A matriz `tiles` é preenchida com os objetos `Tile`, que são criados pelo método `LoadTile`, que é chamado para cada posição do mapa. O método `LoadTile` é responsável por criar um objeto `Tile` para uma determinada posição no mapa, dependendo do tipo de caractere que está presente nessa posição. Por exemplo, se o caractere for '.' o método retorna um `Tile` vazio que pode ser atravessado.

O método `LoadExitTile` é chamado quando um 'X' é encontrado no mapa e carrega as informações necessárias para definir a posição da saída. O método `LoadGemTile` é chamado quando um 'G' é encontrado no mapa e carrega informações sobre a posição das gemas que devem ser coletadas. O método `LoadEnemyTile` é chamado quando um dos personagens inimigos é encontrado no mapa e carrega informações sobre a posição desses personagens.

Finalmente, o método `LoadTile` cria e retorna um novo objeto `Tile` com base na textura que foi carregada e no tipo de colisão que foi fornecido. As informações sobre a textura e a colisão são armazenadas no objeto `Tile`, que é retornado ao método `LoadTiles`. Em seguida, o método `LoadTiles` verifica se o mapa é válido, ou seja, se existem informações suficientes para definir um ponto de partida e um ponto de saída. Se não houver informações suficientes, o método lança uma exceção.

**Bounds and collision**

Há três funções que são responsáveis por retornar informações sobre os tiles (peças) que compõem o nível.

`GetCollision(int x, int y)` - Retorna o modo de colisão (collision mode) do tile em uma posição específica (x, y) do nível. Se a posição estiver fora dos limites do nível, o método retorna `TileCollision.Impassable` (impossível de atravessar) para evitar que o personagem saia dos limites do nível. Se a posição estiver dentro dos limites do nível, ele retorna o modo de colisão do tile específico.

`GetBounds(int x, int y)` - Retorna um retângulo que representa o espaço ocupado pelo tile em uma posição específica (x, y) no nível. O retângulo é criado usando as constantes `Tile.Width` e `Tile.Height` para definir as dimensões do tile e a posição x e y é ajustada para que o retângulo cubra completamente o tile.

`Width` e `Height` - Esses são dois métodos que retornam o número de tiles em largura e altura do nível, respectivamente. Eles usam o método `GetLength()` para retornar o tamanho da matriz `tiles`, que contém informações sobre cada tile no nível.

**Update**

Esta classe é responsável por gerenciar o mundo do jogo, incluindo a atualização dos objetos, a detecção de colisão entre eles, e o controle do tempo restante e pontuação.

O método "Update" é usado para atualizar os objetos do mundo do jogo, incluindo o jogador, inimigos e gemas. Ele verifica se o jogador ainda está vivo e se o tempo restante não chegou a zero, e executa a lógica correspondente com base nesses estados. Se o jogador alcançar a saída do nível, o tempo restante é convertido em pontos de pontuação. Se o jogador cair da parte inferior do nível, ele morre.

Os métodos "UpdateGems", "UpdateEnemies", "OnGemCollected", "OnPlayerKilled" e "OnExitReached" lidam com a detecção de colisão e as interações entre os diferentes objetos do jogo. Por exemplo, quando o jogador coleta uma gema, a pontuação aumenta e a gema é removida do mundo do jogo. Se o jogador tocar em um inimigo, ele morre instantaneamente.

Por fim, o método "StartNewLife" é usado para reiniciar o jogo a partir do ponto inicial, permitindo ao jogador tentar novamente o nível.

**Draw**

A função "Draw" desenha todos os elementos na tela, incluindo as camadas do cenário, os personagens (jogador e inimigos) e as gemas.

A primeira parte do código desenha as camadas do cenário que estão atrás dos personagens e das gemas. O loop "for" desenha cada camada (que são armazenadas em um array de texturas chamado "layers") na tela, começando da camada 0 até a camada "EntityLayer".

Depois disso, a função "DrawTiles" é chamada para desenhar os tiles (pequenas imagens que compõem o cenário) na tela. A função percorre todas as posições possíveis dos tiles (altura e largura), verifica se há uma imagem associada àquele tile e, se houver, desenha-a na posição correspondente na tela.

Em seguida, o código desenha as gemas na tela, chamando a função "Draw" de cada uma delas. Depois disso, desenha o jogador e os inimigos, chamando a função "Draw" de cada um deles.

Por fim, o código desenha as camadas do cenário que estão à frente dos personagens e das gemas. O loop "for" desenha cada camada, começando da camada "EntityLayer" até a última camada no array de texturas "layers".

___

##### Player

A classe "Player" representa o personagem controlado pelo jogador no jogo. A classe contém propriedades e métodos que definem o comportamento e as ações do personagem.

Algumas das propriedades da classe incluem "Position" (a posição do personagem na tela), "Velocity" (a velocidade atual do personagem), "Bounds" (a área retangular ocupada pelo personagem), entre outras.

O método "Update" é chamado a cada quadro do jogo e é responsável por atualizar a posição e a velocidade do personagem com base nas entradas do jogador e nas colisões com objetos no jogo. O método "Draw" é responsável por desenhar o personagem na tela.

Além disso, a classe "Player" também contém métodos como "Jump" (para fazer o personagem pular), "TakeDamage" (para reduzir a saúde do personagem) e "Die" (para fazer o personagem morrer e reiniciar o jogo).



____

##### RectangleExtensions

Este código é uma classe de extensão de Rectangle em C# que oferece **duas funções úteis para detectar colisões entre retângulos**.

```cs
public static Vector2 GetIntersectionDepth(this Rectangle rectA, Rectangle rectB)
```

A primeira função é chamada de **"GetIntersectionDepth"** e é usada para calcular a profundidade de interseção entre dois retângulos. Isso permite que se determine a **direção correta para empurrar objetos a fim de resolver as colisões.**

```cs
public static Vector2 GetBottomCenter(this Rectangle rect)
```

A segunda função é chamada de "**GetBottomCenter**" e é usada para obter a posição do centro da borda inferior de um retângulo. Isso é útil para **posicionar objetos no chão ou detectar colisões com o solo**.

___

##### Tile

É responsável pelo **controle da detecção de colisão e pelo comportamento de resposta de uma tile**. Uma **tile** é uma pequena secção retangular que **compõe o mapa do jogo**.

```cs
enum TileCollision
    {
        /// <summary>
        /// A passable tile is one which does not hinder player motion at all.
        /// </summary>
        Passable = 0,

        /// <summary>
        /// An impassable tile is one which does not allow the player to move through
        /// it at all. It is completely solid.
        /// </summary>
        Impassable = 1,

        /// <summary>
        /// A platform tile is one which behaves like a passable tile except when the
        /// player is above it. A player can jump up through a platform as well as move
        /// past it to the left and right, but can not fall down through the top of it.
        /// </summary>
        Platform = 2,
    }
```

O código começa com a definição de um enum chamado **"TileCollision"** que descreve os diferentes tipos de comportamento de colisão de uma tile. Ele tem três valores: **Passable** (passável), **Impassable** (impassável) e **Platform** (plataforma).

```cs
    struct Tile
    {
        public Texture2D Texture;
        public TileCollision Collision;

        public const int Width = 40;
        public const int Height = 32;

        public static readonly Vector2 Size = new Vector2(Width, Height);

        /// <summary>
        /// Constructs a new tile.
        /// </summary>
```

Em seguida, há a definição de uma estrutura chamada **"Tile"**, que armazena a aparência e o comportamento de colisão de uma tile. Ela possui uma textura (representada por um **Texture2D**) e um tipo de colisão (representado pelo **enum TileCollision**).

```cs
  public Tile(Texture2D texture, TileCollision collision)
        {
            Texture = texture;
            Collision = collision;
        }
```

Por fim, há um construtor que recebe uma textura e um tipo de colisão e cria uma nova instância de Tile com esses valores.

___

##### TouchCollectExtensions

O código define uma classe de extensão pública chamada "TouchCollectionExtensions", que contém um método chamado "AnyTouch". Esse método é usado para verificar se há algum toque na tela.

```cs
  public static class TouchCollectionExtensions
```

Dentro do método, é feito um loop em cada localização de toque na coleção passada como parâmetro.

```cs
   public static bool AnyTouch(this TouchCollection touchState)
        {
            foreach (TouchLocation location in touchState)
            {
                if (location.State == TouchLocationState.Pressed || location.State == TouchLocationState.Moved)
                {
                    return true;
                }
            }
            return false;
        }
```

Se alguma localização de toque estiver no estado Pressionado ou Movido, o método retornará verdadeiro. Caso contrário, o método retornará falso.

____

##### VirtualGamePad.cs

Interface do jogo virtual que simula um comando de jogo físico, incluindo botões de direção, botões de ação e um joystick.

```cs
    class VirtualGamePad
    {
        private readonly Vector2 baseScreenSize;
        private Matrix globalTransformation;
        private readonly Texture2D texture;

        private float secondsSinceLastInput;
        private float opacity;

        public VirtualGamePad(Vector2 baseScreenSize, Matrix globalTransformation, Texture2D texture)
        {
            this.baseScreenSize = baseScreenSize;
            this.globalTransformation = Matrix.Invert(globalTransformation);
            this.texture = texture;
            secondsSinceLastInput = float.MaxValue;
        }

        public void NotifyPlayerIsMoving()
        {
            secondsSinceLastInput = 0;
        }
```

O construtor da classe recebe três argumentos: um objeto Vector2 representando o tamanho da tela base, uma matriz de transformação global e um objeto Texture2D que representa a textura do controle de jogo virtual. A classe também mantém um registro de quanto tempo se passou desde a última entrada do jogador e um valor de opacidade que controla a transparência do controle de jogo virtual.

```cs
        public void Update(GameTime gameTime)
        {
            var secondsElapsed = (float)gameTime.ElapsedGameTime.TotalSeconds;
            secondsSinceLastInput += secondsElapsed;

            //If the player is moving, fade the controls out
            // otherwise, if they haven't moved in 4 seconds, fade the controls back in
            if (secondsSinceLastInput < 4)
                opacity = Math.Max(0, opacity - secondsElapsed * 4);
            else
                opacity = Math.Min(1, opacity + secondsElapsed * 2);
        }

        public void Draw(SpriteBatch spriteBatch)
        {
            var spriteCenter = new Vector2(64, 64);
            var color = Color.Multiply(Color.White, opacity);

            spriteBatch.Draw(texture, new Vector2(64, baseScreenSize.Y - 64), null, color, -MathHelper.PiOver2, spriteCenter, 1, SpriteEffects.None, 0);
            spriteBatch.Draw(texture, new Vector2(192, baseScreenSize.Y - 64), null, color, MathHelper.PiOver2, spriteCenter, 1, SpriteEffects.None, 0);
            spriteBatch.Draw(texture, new Vector2(baseScreenSize.X - 128, baseScreenSize.Y - 128), null, color, 0, Vector2.Zero, 1, SpriteEffects.None, 0);
        }
```

A classe tem métodos para notificar quando o jogador está se movendo, atualizar a opacidade do controle de jogo virtual com base no tempo desde a última entrada do jogador e desenhar o controle de jogo virtual na tela.

```cs
        public GamePadState GetState(TouchCollection touchState, GamePadState gpState)
```

A classe também tem um método chamado "GetState" que recebe um objeto TouchCollection que representa a entrada de toque do jogador e um objeto GamePadState que representa o estado atual do controle de jogo físico.

O método combina as informações desses dois objetos para gerar um novo objeto GamePadState que pode ser usado pelo jogo para determinar como o jogador está interagindo com o jogo.

```
 var gpButtons = gpState.Buttons;
            buttonsPressed |= (gpButtons.A == ButtonState.Pressed ? Buttons.A : 0);
            buttonsPressed |= (gpButtons.B == ButtonState.Pressed ? Buttons.B : 0);
            buttonsPressed |= (gpButtons.X == ButtonState.Pressed ? Buttons.X : 0);
            buttonsPressed |= (gpButtons.Y == ButtonState.Pressed ? Buttons.Y : 0);

            buttonsPressed |= (gpButtons.Start == ButtonState.Pressed ? Buttons.Start : 0);
            buttonsPressed |= (gpButtons.Back == ButtonState.Pressed ? Buttons.Back : 0);

            buttonsPressed |= gpState.IsButtonDown(Buttons.DPadDown) ? Buttons.DPadDown : 0;
            buttonsPressed |= gpState.IsButtonDown(Buttons.DPadLeft) ? Buttons.DPadLeft : 0;
            buttonsPressed |= gpState.IsButtonDown(Buttons.DPadRight) ? Buttons.DPadRight : 0;
            buttonsPressed |= gpState.IsButtonDown(Buttons.DPadUp) ? Buttons.DPadUp : 0;

            buttonsPressed |= (gpButtons.BigButton == ButtonState.Pressed ? Buttons.BigButton : 0);
            buttonsPressed |= (gpButtons.LeftShoulder == ButtonState.Pressed ? Buttons.LeftShoulder : 0);
            buttonsPressed |= (gpButtons.RightShoulder == ButtonState.Pressed ? Buttons.RightShoulder : 0);

            buttonsPressed |= (gpButtons.LeftStick == ButtonState.Pressed ? Buttons.LeftStick : 0);
            buttonsPressed |= (gpButtons.RightStick == ButtonState.Pressed ? Buttons.RightStick : 0);

            var buttons = new GamePadButtons(buttonsPressed);

            return new GamePadState(gpState.ThumbSticks, gpState.Triggers,
```
