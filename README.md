# OpenGl.test

이번 주전자 과제를 하면서 OpenGL를 어떻게 활용하는지 어떤 프로그램을 사용하는지 알 수 있게 되어 좋았습니다. 
막힌 부분도 많았지만 찾아보고 어떻게 해결해야할지 스스로 발전할 수 있는 계기가 되었습니다.


#include <iostream>
#include <GL/freeglut.h>


GLuint textureID;


void loadTexture() {
    
}


void display() {
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glLoadIdentity();

   
    glEnable(GL_TEXTURE_2D);
    glBindTexture(GL_TEXTURE_2D, textureID);

    glBegin(GL_QUADS);
        glTexCoord2f(0.0f, 0.0f);
        glVertex2f(-1.0f, -1.0f);

        glTexCoord2f(1.0f, 0.0f);
        glVertex2f(1.0f, -1.0f);

        glTexCoord2f(1.0f, 1.0f);
        glVertex2f(1.0f, 1.0f);

        glTexCoord2f(0.0f, 1.0f);
        glVertex2f(-1.0f, 1.0f);
    glEnd();

    glDisable(GL_TEXTURE_2D);

    glutSwapBuffers();
}


void reshape(int w, int h) {
    glViewport(0, 0, w, h);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    glOrtho(-1.0, 1.0, -1.0, 1.0, -1.0, 1.0);
    glMatrixMode(GL_MODELVIEW);
    glLoadIdentity();
}


void init() {
    glClearColor(0.0f, 0.0f, 0.0f, 1.0f); 
    glEnable(GL_DEPTH_TEST);

    
    loadTexture();
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
    glutInitWindowSize(800, 600);
    glutCreateWindow("Image Rotation");

    glutDisplayFunc(display);
    glutReshapeFunc(reshape);

    init(); 

    glutMainLoop();

    return 0;
}
