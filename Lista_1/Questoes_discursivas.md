1. O que é GLSL? Quais são os dois tipos de shaders que devem estar presentes no pipeline programável da versão que trabalhamos em aula e o que eles processam?
        GLSL é a linguagem específica do OpenGL usada para escrever shaders. Os dois shaders obrigatórios no pipeline programável são o "Vertex Shader" e o "Fragment Shader". O Vertex Shader processa a posição e outros atributos dos vértices, enquanto o Fragment Shader lida com a cor e outras propriedades de cada fragmento (pixel).

2. O que são primitivas gráficas? Como os vértices são armazenados no OpenGL?
        Primitivas gráficas são formas básicas como pontos, linhas e triângulos, que são enviadas para o processamento através de uma chamada de desenho (drawcall). No OpenGL, os vértices dessas primitivas são armazenados usando os Vertex Buffer Objects (VBOs), que são arrays contendo os dados dos vértices.

3. Explique o que são VBO, VAO e EBO, e como eles se relacionam.
        VBO (Vertex Buffer Object): um array que contém os dados dos vértices, geralmente armazenando informações como posições, normais e coordenadas de textura.
        VAO (Vertex Array Object): armazena a configuração de como os vértices estão organizados no VBO, facilitando a reutilização de configurações de desenho.
        EBO (Element Buffer Object): usado para otimizar o uso de vértices, evitando a duplicação de dados ao permitir a reutilização de vértices por meio de índices.

        O VAO organiza e gerencia as ligações do VBO e EBO, garantindo que os dados dos vértices sejam interpretados corretamente para o desenho.

4. Análise do código fonte do projeto "Hello Triangle" e como ele se relaciona com shaders, VBOs e VAO.
        Ao analisar o código, é possível identificar como os shaders são usados para controlar a aparência dos triângulos na tela, enquanto os VBOs armazenam os dados dos vértices e o VAO gerencia como esses dados são utilizados durante o desenho. Este exercício não precisa ser entregue.

5. Desenhe 2 triângulos na tela. Desenhe-os nas seguintes formas:
        a. Apenas com o preenchimento do polígono
        b. Apenas com o contorno
        c. Apenas com pontos
        d. Usando as três formas juntas

6. Configuração dos buffers:
        A configuração dos buffers para este caso é relativamente simples e não difere muito do padrão. Abaixo está um exemplo de código resumido, onde algumas funções foram omitidas para manter o foco nos buffers.

VBO

C++

float vertices[] = {
     0.5f,  0.8f, 0.0f,
    -0.8f, -0.8f, 0.0f,
     0.7f, -0.4f, 0.0f
};  

unsigned int VBO;
glGenBuffers(1, &VBO);  
glBindBuffer(GL_ARRAY_BUFFER, VBO); 
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);

VAO

C++

unsigned int VAO;
glGenVertexArrays(1, &VAO);

// Inicializando o VAO
glBindVertexArray(VAO);

// Vinculando o VBO e copiando os dados dos vértices para o buffer
glBindBuffer(GL_ARRAY_BUFFER, VBO);
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);

// Definindo como os dados dos vértices devem ser interpretados
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
glEnableVertexAttribArray(0);  

//[...]

// Desenhando o objeto
glUseProgram(shaderProgram);
glBindVertexArray(VAO);
drawTriangleFunction();

EBO

    Neste exemplo, um EBO não é necessário, pois não estamos repetindo vértices o suficiente para justificar seu uso.